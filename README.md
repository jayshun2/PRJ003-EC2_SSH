# EC2 Linux Instance and SSH Into It

## Overview

This project walks through launching a Linux-based EC2 instance on Amazon Web Services (AWS) and securely connecting to it via SSH. This is a foundational skill for anyone getting started with AWS or cloud infrastructure. You'll gain practical experience with virtual machines, secure access control, and basic network configuration in the AWS environment.

## Architecture

The following AWS components are used:

* **Amazon EC2 (Elastic Compute Cloud):** Hosts the virtual Linux server.
* **Amazon VPC (Virtual Private Cloud):** Provides the isolated network environment.
* **Security Groups:** Firewall rules that allow inbound SSH (port 22) traffic.
* **Key Pair:** Used to authenticate and securely connect to your instance.

Together, these services enable you to provision a secure, cloud-based Linux environment that you can access from your local machine.

## Getting Started

### Prerequisites

* AWS account with Free Tier access
* SSH client installed (Terminal on macOS/Linux, WSL or PuTTY on Windows)
* Basic familiarity with the command line

### Steps

1. **Create a Key Pair**

   * In the AWS Console, navigate to **EC2 > Network & Security > Key Pairs**.
   * Create a new key pair (e.g., `ec2-keypair`) and choose `.pem` format.
   * Download the private key file and store it securely.

2. **Launch an EC2 Instance**

   * Go to **EC2 > Instances > Launch Instance**.
   * Set the name (e.g., `my-ec2-linux`).
   * Choose **Amazon Linux 2023 (64-bit x86)** as the AMI.
   * Select **t2.micro** (Free Tier eligible).
   * Under **Key pair login**, select your key pair.
   * In **Network settings**, allow SSH (port 22) from your IP address.
   * Launch the instance.

3. **Retrieve the Public IP**

   * In the EC2 dashboard, select your instance.
   * Copy the **Public IPv4 address** for later use in the SSH connection.

## Usage

1. Open your terminal.
2. Navigate to the directory where your `.pem` file is saved:

   ```bash
   cd ~/Downloads  # or wherever the file is
   ```
3. Modify the file permissions:

   ```bash
   chmod 600 ec2-keypair.pem
   ```
4. Connect to the instance using the provided command:

   ```bash
   ssh -i ec2-keypair.pem ec2-user@<your-public-ip>
   ```
5. Type `yes` if prompted to trust the host.
6. You're now inside your EC2 instance!

To verify the system is working:

```bash
uname -a
top
```

Use `exit` to safely disconnect.

## Cleanup

To avoid charges:

1. Go to the EC2 dashboard.
2. Select your instance.
3. Click **Instance state → Terminate instance**.
4. Confirm the termination.
5. Optionally, delete the key pair from **EC2 > Key Pairs**.

## Optional Enhancements

* Install a web server (Apache, Nginx) on the instance.
* Assign an Elastic IP for persistent access.
* Attach IAM roles to the instance for secure access to services like S3.
* Use AWS CLI or Terraform to automate this entire setup.

## License

MIT License
