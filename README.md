# AWS VPC, EC2 & Linux Administration Lab

## Project Overview

This project demonstrates hands-on experience with AWS cloud infrastructure, networking, Linux system administration, and Bash scripting. I designed and configured a custom AWS Virtual Private Cloud (VPC), deployed an Ubuntu EC2 instance, configured security groups and routing, troubleshot SSH connectivity, and completed Linux administration tasks.

The goal was to gain practical experience with core cloud computing concepts, including network isolation, server deployment, remote access, file management, permissions, scripting, and compression.

## Technologies and Tools

- **Cloud Platform:** Amazon Web Services (AWS)
- **AWS Services:** VPC, EC2, Internet Gateway, Route Tables, Security Groups, EC2 Instance Connect, EBS
- **Operating System:** Ubuntu Server 24.04 LTS
- **Networking:** IPv4, CIDR, TCP/IP, SSH, HTTP, HTTPS, SMTP
- **Linux Tools:** Bash, Nano, APT, Tree, TAR, Gzip
- **Version Control:** Git and GitHub

## 1. AWS VPC Architecture and Networking

I designed an AWS VPC architecture with public and private subnets, an Internet Gateway, a NAT Gateway, and separate route tables.

I then implemented the VPC, subnets, Internet Gateway, and route tables in AWS.

### VPC Configuration

| Component | Configuration |
|---|---|
| VPC Name | `cloud-lab-vpc` |
| VPC CIDR | `10.0.0.0/16` |
| Public Subnet | `cloud-lab-public-subnet` |
| Public Subnet CIDR | `10.0.0.0/24` |
| Private Subnet | `cloud-lab-private-subnet` |
| Internet Gateway | `cloud-lab-igw` |
| Public Route Table | `cloud-lab-public-rt` |
| Private Route Table | `cloud-lab-private-rt` |

### Public Subnet Routing

The public route table was configured with:

- `10.0.0.0/16 → local`
- `0.0.0.0/0 → Internet Gateway`

This provides a path to the internet for resources with appropriate public IP addresses and security configurations.

### Private Subnet Routing

The private route table was configured with:

- `10.0.0.0/16 → local`

This supports internal VPC routing without a direct internet route.

**Note:** A NAT Gateway was included in the architecture drawing but was not deployed in AWS to avoid unnecessary charges.

## 2. EC2 Instance Deployment

I launched an Ubuntu Linux virtual server using Amazon EC2 and configured the instance within my custom VPC.

### EC2 Configuration

| Setting | Configuration |
|---|---|
| Instance Name | `cloud-lab-ubuntu` |
| Operating System | Ubuntu Server 24.04 LTS |
| Architecture | 64-bit x86 |
| Instance Type | `t3.micro` |
| Storage | 8 GiB gp3 EBS |
| VPC | `cloud-lab-vpc` |
| Subnet | `cloud-lab-public-subnet` |
| Security Group | `cloud-lab-sg` |
| SSH Authentication | EC2 Key Pair |

The instance was configured with a public IPv4 address to support remote administrative access.

## 3. Security Group Configuration

I created an EC2 security group to control inbound and outbound network traffic.

### Inbound Rules

| Protocol | Port | Source |
|---|---|---|
| SSH | 22 | Restricted IP address |
| HTTP | 80 | Anywhere IPv4 |
| HTTPS | 443 | Anywhere IPv4 |
| SMTP | 25 | Restricted IP address |

I also configured an additional SSH rule using the regional AWS-managed EC2 Instance Connect prefix list.

These rules allowed me to practice managing network access to cloud resources.

## 4. SSH Connectivity and Troubleshooting

During the deployment, I encountered an SSH connection error when attempting to connect through EC2 Instance Connect.

I investigated the issue by reviewing the instance state, EC2 status checks, and security group rules.

### Troubleshooting Process

1. Confirmed that the Ubuntu EC2 instance was running.
2. Verified that all three EC2 status checks passed.
3. Reviewed inbound SSH rules and their source restrictions.
4. Added the appropriate AWS EC2 Instance Connect prefix list to the security group.
5. Successfully established an SSH connection through the AWS browser-based terminal.

This exercise helped me understand how security groups and network access rules affect remote connectivity.

## 5. Linux Directory and File Management

After connecting to Ubuntu, I created a project directory containing source code and documentation folders.

### Commands Used

```bash
mkdir project
cd project
mkdir src docs
touch src/main.py
touch docs/README.md
```

I installed the `tree` utility using APT:

```bash
sudo apt update
sudo apt install tree -y
```

I then verified the directory structure:

```bash
tree
```

### Directory Structure

```text
project/
├── docs/
│   └── README.md
└── src/
    ├── main.py
    └── run.sh
```

## 6. Linux File Permissions

I practiced managing file permissions with `chmod` and verifying them using `ls -l`.

### Commands Used

```bash
chmod +x src/main.py
chmod 444 docs/README.md
ls -l src
ls -l docs
```

The `chmod +x` command added executable permissions to `main.py`, while `chmod 444` made `README.md` read-only for the owner, group, and other users.

This exercise demonstrated the importance of controlling file access on Linux systems.

## 7. Bash Scripting

I created a Bash script named `run.sh` using the Nano text editor.

### Script

```bash
#!/bin/bash
echo "Hello, World!"
```

I made the script executable and ran it:

```bash
chmod +x src/run.sh
./src/run.sh
```

### Output

```text
Hello, World!
```

The script executed successfully on the Ubuntu EC2 instance.

This introduced me to Bash scripting, executable permissions, and basic command-line automation.

## 8. File Editing with Nano

I used the Nano text editor to modify `README.md`.

Because the file was initially read-only, I temporarily changed its permissions:

```bash
chmod u+w docs/README.md
nano docs/README.md
```

After editing and saving the file, I restored its read-only permissions:

```bash
chmod 444 docs/README.md
```

I verified the saved content using:

```bash
cat docs/README.md
```

## 9. File Archiving and Compression

I practiced creating and compressing Linux archives using TAR and Gzip.

### Commands Used

```bash
cd ~
tar -cvf project.tar project
gzip project.tar
ls -lh project.tar.gz
```

### Results

- Created an archive named `project.tar`.
- Compressed the archive into `project.tar.gz`.
- Verified that the compressed archive was created successfully.
- Final compressed file size: **361 bytes**.

This exercise demonstrated how to package and compress files for storage, transfer, and backup.

## 10. Key Challenges and Solutions

### Challenge 1: Linux Package Installation

**Problem:** Ubuntu initially returned `Unable to locate package tree`.

**Solution:** I refreshed the package lists using `sudo apt update` and then installed the package successfully.

### Challenge 2: SSH Connection Failure

**Problem:** EC2 Instance Connect initially failed to establish an SSH connection.

**Solution:** I verified EC2 instance health and updated the security group to allow the appropriate EC2 Instance Connect traffic.

### Challenge 3: Linux File Permissions

**Problem:** The README file was configured as read-only, preventing normal editing.

**Solution:** I temporarily granted owner write permission, edited the file, and restored its original permissions.

## 11. Project Results

Successfully completed the following tasks:

- Designed and implemented a custom AWS VPC network.
- Created and configured public and private subnets.
- Configured an Internet Gateway and route tables.
- Created security group rules for multiple network protocols.
- Deployed an Ubuntu EC2 instance.
- Troubleshot SSH connectivity and accessed the Linux server.
- Managed Linux directories, files, and permissions.
- Created and executed a Bash script.
- Edited documentation using Nano.
- Archived and compressed project files.

## 12. Skills Developed

This project strengthened my understanding of AWS infrastructure, virtual networking, EC2 deployment, Linux administration, SSH troubleshooting, access controls, Bash scripting, and command-line file management.

It provided foundational hands-on experience with the infrastructure and operating-system tools commonly used in Cloud Engineering and DevOps environments.

## Future Improvements

Potential next steps include:

- Provisioning infrastructure using Terraform.
- Creating reusable Bash automation scripts.
- Implementing AWS CloudWatch monitoring and alarms.
- Configuring IAM roles and least-privilege access.
- Deploying a simple web application to EC2.
- Automating EC2 configuration using Ansible.
- Building a multi-Availability Zone architecture.
- Implementing CI/CD workflows using GitHub Actions.

---

**Project Type:** Hands-on Cloud/DevOps Engineering Lab

**Cloud Provider:** Amazon Web Services (AWS)

**Operating System:** Ubuntu Server 24.04 LTS

**Focus:** AWS Networking, EC2, Linux Administration, SSH Troubleshooting, and Bash Scripting
