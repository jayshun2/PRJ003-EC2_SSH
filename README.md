# PRJ003-EC2_SSH
# EC2 Linux Instance and SSH Into It

## Overview

This project demonstrates how to launch a Linux-based EC2 instance on Amazon Web Services (AWS) and connect to it using SSH. It’s an essential first step for anyone learning cloud computing or building applications in the cloud. You'll gain hands-on experience working with AWS infrastructure and learn how to securely access and manage remote servers.

## Architecture

The core AWS services used in this project include:

- **Amazon EC2 (Elastic Compute Cloud):** Provides the virtual Linux server you launch and connect to.
- **Amazon VPC (Virtual Private Cloud):** Creates an isolated network environment for your EC2 instance to run in.
- **Security Groups:** Acts as a firewall, controlling inbound and outbound traffic — in this case, enabling SSH (port 22) access.
- **Key Pair:** A public-private key mechanism used to securely authenticate access to the instance.

These components work together to spin up a cloud-based Linux server that can be safely accessed from your local machine using SSH.

## Getting Started

### Prerequisites

- AWS Free Tier account
- Basic terminal knowledge (macOS, Linux, or Windows with WSL or PuTTY)
- SSH client installed
- A modern web browser

### Steps

1. **Create a Key Pair**
   - In the AWS Console, search for “Key Pairs” and create a new key pair named `ec2-keypair`.
   - Choose `.pem` format and download the private key to a safe location.

2. **Launch an EC2 Instance**
   - Go to the EC2 dashboard and click "Launch Instance".
   - Name it `my-ec2-linux`.
   - Choose **Amazon Linux 2023** as the AMI.
   - Select `t2.micro` as the instance type (Free Tier eligible).
   - Use the key pair you created (`ec2-keypair`) for login.
   - Under Network Settings, allow SSH (port 22) from your IP or 0.0.0.0/0 (less secure).
   - Launch the instance.

3. **Retrieve the Public IP**
   - Go to the EC2 dashboard, select your instance, and note the public IPv4 address.

## Usage

Once your instance is running:

1. Open your terminal and navigate to the directory containing your `.pem` file.
2. Run the SSH command:
   ```bash
   ssh -i ec2-keypair.pem ec2-user@<your-public-ip>
3. If prompted, type yes to continue.
4. You are now connected to your EC2 instance!


To verify everything is working:
Run uname -a or top to interact with the Linux system.
Use exit to safely disconnect from the session.


###Cleanup
To avoid unnecessary charges:
1. Go to the EC2 dashboard.
2. Select your instance.
3. Click Instance state → Terminate instance.
4. Confirm termination.
5. Optionally, delete your key pair from the "Key Pairs" section of the EC2 console.


###Optional Enhancements

Install and configure a web server (Apache or Nginx).
Assign an Elastic IP to make your instance’s address persistent.
Add IAM roles to allow your instance to access other AWS services like S3.
Automate the provisioning process using Terraform or AWS CLI.


###License
MIT License

