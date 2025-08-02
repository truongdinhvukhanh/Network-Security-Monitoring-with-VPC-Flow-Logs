---
title : "Create the Ingest Pipeline"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

{{% notice note %}}
This step is crucial for preparing your OpenSearch domain to properly ingest and analyze VPC Flow Log data. You will first verify access to OpenSearch Dashboards via an SSH tunnel through your Bastion Host. Following this, you will create and test an ingest pipeline (**vpc-flow-log-pipeline**). This pipeline uses a Grok processor to parse the raw, unstructured VPC Flow Log messages into distinct, searchable fields, making the data highly valuable for security analysis and network monitoring within OpenSearch.
{{% /notice %}}

#### Verify Access to OpenSearch Dashboards
Now that your OpenSearch domain is active, you'll need to verify that you can access OpenSearch Dashboards.
1. **Set Up SSH Tunnel to Access OpenSearch Dashboards**
    - **Open a terminal or command prompt on your local machine**
    - **Create an SSH tunnel through your Bastion Host**        
        ```powershell
        ssh -i "your-key.pem" -L 9200:your-opensearch-endpoint:443 ec2-user@your-bastion-host-ip
        ```        
        - Replace `your-key.pem` with the path to your key file
        - Replace `your-opensearch-endpoint` with your OpenSearch domain endpoint (without `https://` and `/_dashboards`) that you copied in previous step            
            ![image.png](/images/5/5.2/image.png)            
        - Replace `your-bastion-host-ip` with your Bastion Host's public IP        
        ![image.png](/images/5/5.2/image%201.png)        
    - Keep this terminal window open while you perform the following steps

2. **Access OpenSearch Dashboards**
    - Open your web browser, enter the URL: `https://localhost:9200/_dashboards/`    
    ![image.png](/images/5/5.2/image%202.png)    
    ![image.png](/images/5/5.2/image%203.png)    
3. **Verify Your Admin Access**
    - **Explore the OpenSearch Dashboards Interface**
        - After logging in, you should see the OpenSearch Dashboards home page
        - Take a moment to familiarize yourself with the interface
    - **Check Cluster Health**
        - In the left navigation menu, click on **Dev Tools**          
            ![image.png](/images/5/5.2/image%204.png)            
        - In the Console, run the following command:            
            ```
            GET _cluster/health
            ```            
        - The response should show the health status of your cluster (ideally "green")            
            ![image.png](/images/5/5.2/image%205.png)            
4. Create the Ingest Pipeline    
    Execute this command in the Dev Tools console to create your parsing pipeline:    
    ```json
    PUT _ingest/pipeline/vpc-flow-log-pipeline
    {
      "description": "Pipeline to parse VPC Flow Log data",
      "processors": [
        {
          "grok": {
            "field": "message",
            "patterns": [
              "%{NUMBER:version:int} %{NUMBER:account_id} (%{NOTSPACE:interface_id}|-) (%{IP:srcaddr}|-) (%{IP:dstaddr}|-) (%{NUMBER:srcport:int}|-) (%{NUMBER:dstport:int}|-) (%{NUMBER:protocol:int}|-) (%{NUMBER:packets:int}|-) (%{NUMBER:bytes:long}|-) (%{NUMBER:start:long}|-) (%{NUMBER:end:long}|-) (%{WORD:action}|-) (%{WORD:log_status}|-)"
            ]
          }
        },
        {
          "script": {
            "description": "Convert dash values to null",
            "source": """
              def fields = ['interface_id', 'srcaddr', 'dstaddr', 'srcport', 'dstport', 'protocol', 'packets', 'bytes', 'start', 'end', 'action', 'log_status'];
              for (def field : fields) {
                if (ctx.containsKey(field) && ctx[field] == '-') {
                  ctx[field] = null;
                }
              }
            """
          }
        },
        {
          "remove": {
            "field": "message"
          }
        }
      ]
    }    
    ```    
    This pipeline:    
    - Uses a **Grok processor** to parse the space-delimited VPC Flow Log format
    - Extracts 14 individual fields with appropriate data types
    - Removes the original **message** field after parsing    
    ![image.png](/images/5/5.2/image%206.png)    
5. Test the Pipeline    
    Before applying it to your data, test the pipeline with your sample data:    
    ```json
    POST _ingest/pipeline/vpc-flow-log-pipeline/_simulate
    {
      "docs": [
        {
          "_source": {
            "message": "2 509069525939 eni-06dbfc5864eff22c5 10.0.2.79 10.0.2.216 443 56618 6 4 4734 1753442090 1753442117 ACCEPT OK"
          }
        }
      ]
    }
    ```    
    The response should show your data parsed into individual fields:    
    ![image.png](/images/5/5.2/image%207.png)    
6. Apply Pipeline to New Data    
    For **new incoming data**, create an index template that automatically applies the pipeline:    
    ```json
    PUT _index_template/vpc-flow-logs-template
    {
      "index_patterns": ["vpc-flow-logs-*"],
      "template": {
        "settings": {
          "default_pipeline": "vpc-flow-log-pipeline"
        },
        "mappings": {
          "properties": {
            "version": { "type": "keyword" },
            "account_id": { "type": "keyword" },
            "interface_id": { "type": "keyword" },
            "srcaddr": { "type": "ip" },
            "dstaddr": { "type": "ip" },
            "srcport": { "type": "integer" },
            "dstport": { "type": "integer" },
            "protocol": { "type": "integer" },
            "packets": { "type": "integer" },
            "bytes": { "type": "long" },
            "start": { "type": "date", "format": "epoch_second" },
            "end": { "type": "date", "format": "epoch_second" },
            "action": { "type": "keyword" },
            "log_status": { "type": "keyword" }
          }
        }
      }
    }
    ```    
    ![image.png](/images/5/5.2/image%208.png)    
- Keep this window open while you perform the following steps