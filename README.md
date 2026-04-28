# Managing-Cluster-with-EKS 
PROJECT BY EZE SOMTOCHUKWU


AWS CLI + EKS Setup Guide

This guide explains how to install and configure AWS CLI, install eksctl, authenticate AWS access, and prepare required AWS resources like S3 buckets and EC2 key pairs for Kubernetes deployments.

Install AWS CLI
Windows Installation

Download and install AWS CLI v2:

 https://aws.amazon.com/cli/

After installation, verify:

#aws --version

Expected output:

aws-cli/2.x.x Python/...
Install eksctl (EKS CLI Tool)
Windows Installation (Chocolatey method)
#choco install eksctl

OR manual installation:
Extract and add eksctl.exe to PATH

**Verify installation:**

#eksctl version

**Configure AWS Credentials**

Run the following command to authenticate your AWS CLI:

#aws configure

**You will be prompted to enter:
**
AWS Access Key ID: YOUR_ACCESS_KEY

AWS Secret Access Key: YOUR_SECRET_KEY

Default region name: us-east-1

Default output format: json

** Verify authentication
**
#aws sts get-caller-identity

If successful, you will see your AWS account details.

**Create an S3 Bucket (for storage use cases)
**
S3 buckets are often used for storing Terraform state files, logs, or application assets.

aws s3 mb s3://your-unique-bucket-name

Example:

aws s3 mb s3://my-eks-project-bucket-2026

List buckets:

#aws s3 ls

**Create EC2 Key Pair (Required for EKS Node Access)
**
This key allows SSH access to worker nodes if enabled.

aws ec2 create-key-pair --key-name eks-key --query "KeyMaterial" --output text > eks-key.pem
 Secure your key file (IMPORTANT)

**On Windows (PowerShell):
**
#icacls eks-key.pem /inheritance:r
#icacls eks-key.pem /grant:r "%USERNAME%:R"

**On Linux/Mac:
**
#chmod 400 eks-key.pem
 Example EKS Cluster Configuration

Create a file named eks-cluster.yaml:



**Run:
**
#eksctl create cluster -f eks-cluster.yaml



<img width="1903" height="1017" alt="ScreenShot_4_27_2026_11_36_53_PM" src="https://github.com/user-attachments/assets/b584e940-4689-4b95-b4f9-7210623137ec" />

