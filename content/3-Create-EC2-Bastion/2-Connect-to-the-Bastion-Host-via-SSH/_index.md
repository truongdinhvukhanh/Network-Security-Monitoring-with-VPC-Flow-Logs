---
title : "Connect to the Bastion Host via SSH"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

{{% notice note %}}
This step outlines how to securely connect to your **NSM-Bastion** host using SSH. Establishing an SSH connection to the Bastion Host is crucial because it acts as a secure jump server, allowing you to then access other resources in your private subnets (which are not directly accessible from the internet). This ensures that your internal infrastructure remains isolated and protected, with all access points carefully controlled through the Bastion Host.
{{% /notice %}}

1. Open Command Prompt with Administrator privileges
2. Remove all current access permissions to the file:    
    ```powershell
    icacls "<your-path-to-keypairfile>" /inheritance:r
    ```    
    ```powershell
    icacls "<your-path-to-keypairfile>" /remove:g *S-1-1-0
    ```    
    - Replace `<your-path-to-keypairfile>` with the actual path to your `NSM-Key.pem` file
    - `/inheritance:r`: Disables inheritance of permissions from the parent folder
    - `/remove:g *S-1-1-0`: Removes permissions for the "Everyone" group    
    ![image.png](../images/3/3.2/image.png)    
3. Grant Read & Execute permissions to the current user:    
    ```powershell
    icacls "<your-path-to-keypairfile>" /grant:r <YourName>:(RX)
    ```    
    - Replace `<YourName>` with your actual Windows username
    - `(RX)`: Stands for Read & Execute
    - If you are unsure of your username, you can run the `whoami` command to find it. For example, if the result is `users/aws`, replace `<YourName>` with `aws`
    ![image.png](../images/3/3.2/image%201.png)  
4. Check assigned permissions:    
    ```powershell
    icacls "<your-path-to-keypairfile>"
    ```    
    ![image.png](../images/3/3.2/image%202.png)    
5. Connect to the Bastion Host via SSH:    
    ```powershell
    ssh -i "<your-path-to-keypairfile>" ec2-user@<Public-IP>
    ```    
    - Replace `<your-path-to-keypairfile>` with the path to your `NSM-Key.pem` file.
    - Replace `<Public-IP>` with the Public IP address of your EC2 instance.   
    **First-time connection prompt:**
    The first time you connect, you will be asked "Are you sure you want to continue connecting (yes/no/[fingerprint])?". Type `yes`    
    ![image.png](../images/3/3.2/image%203.png)    
    You have successfully completed the Bastion EC2 creation and verification.