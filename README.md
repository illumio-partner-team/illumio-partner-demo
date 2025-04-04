# Terraform AWS & Azure Deployment

## Requirements
- **Terraform**: [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- **AWS CLI**: [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- **Azure CLI**: [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
- **AWS and Azure Credentials**
- *(Optional)* **Git for Windows**: [Download Git for Windows](https://gitforwindows.org/) - Provides a BASH emulation used to run Git from the command line. *NIX users will find the BASH emulation similar to the native `git` command in Linux/Unix environments.

---

## Folder Structure
This repository contains two folders:
- `AWS/` - Contains Terraform files for provisioning AWS resources.
- `Azure/` - Contains Terraform files for provisioning Azure resources.

---

## Deploying AWS Resources
### Steps to Run Terraform in AWS Folder:
1. Navigate to the `AWS/` folder.
2. Run the following Terraform commands:
   ```sh
   terraform init
   terraform plan
   terraform apply
   ```

### Handling S3 Bucket Errors
If you encounter the following error:
```sh
Error: creating S3 Bucket (us-east-1-730335348333): BucketAlreadyExists
│
│   with aws_s3_bucket.s3bucket,
│   on S3_Bucket_Flow_Logs_aws.tf line 1, in resource "aws_s3_bucket" "s3bucket":
│    1: resource "aws_s3_bucket" "s3bucket" {
```
You need to manually **empty and delete** the existing S3 bucket in your AWS account before re-running `terraform apply`.
After terraform completion, you should have 13 EC2 instances created with 2 VPCs and all its related networking resources.

---

## Deploying Azure Resources
### Steps to Run Terraform in Azure Folder:
1. Navigate to the `Azure/` folder.
2. Run the following Terraform commands:
   ```sh
   terraform init
   terraform plan
   terraform apply
   ```

---

## CORE Data Center Onboarding
### For Illumio INTERNAL SEs ONLY

#### Access the VAAS Instance
Via VPN, navigate to your chosen VAAS instance:
- [VAAS Instance 1](https://vaas-sedemos2.poc.segmentationpov.com/)
- [VAAS Instance 2](https://vaas.poc.segmentationpov.com/)

#### Create a New Instance
Provide the following details:
- **Instance Name**
- **Owner First Name**
- **Owner Last Name**
- **Email Address**
- **Password to Delete**
- **Confirm Password to Delete**

#### Login to Illumio Console for the remaining details
1. Log in to your [Illumio Console](https://console.illum.io/#/login).
2. Select [My API Keys](https://console.illum.io/#/apikeys) under your logged-in username menu (top left).
3. Enter the following details:
   - **Management Server (FQDN:Port format)**: This should be the address listed on your PCE API Endpoint (e.g., `poc3.illum.io:443`).
   - **Email or API User**: Add/Create an API Key in your PCE console under **My API Keys**.
   - **Password or API Key**: Use the API Key password generated from your PCE console.
   - **Confirm Password or API Key**.
   - **Org ID**: Use the Org ID on the API.
4. Click **Submit** and let Vensim complete the process.

---

## Cleaning Up AWS & Azure Environments
If you lose your Terraform `tfstate` file, you must manually clean up AWS and Azure environments to avoid unnecessary cloud costs. Additionally, check for duplicate resources if errors occur.

### Cleaning Up AWS
- This is a **manual process**.
- Delete **VPC1** and **VPC2**, along with all their dependencies.

### Cleaning Up Azure
- Navigate to the **testdrive Resource Group** in Azure.
- Delete **all items** within the testdrive Resource Group.
- Afterward, delete the **Resource Group** itself.

---

## Notes
- Ensure your AWS and Azure credentials are properly configured before running Terraform.
- Always review the Terraform plan output before applying changes.
- Use caution when modifying or destroying cloud resources.


# 🔐 Authenticating Terraform to AWS using API Keys
To authenticate Terraform to AWS using an **Access Key** and **Secret Key**, follow these steps to create an IAM user with the appropriate permissions.

## 1. ✅ Create an AWS IAM User for Terraform
1. Sign in to the [AWS Console](https://console.aws.amazon.com/iam/).
2. Navigate to **"Users"** under **Access Management**.
3. Click **"Add users"**.
4. Set a username (e.g., `terraform-user`).
5. Under **Permissions**, select:
   - ✅ **Attach policies directly**
   - ✅ Choose **AdministratorAccess**
6. Click **Next: Tags**, then **Next: Review**, and finally **Create user**.

## 2. 🔑 Create Access Key
After creating the user:
- Go to the **Security credentials** tab for the new user.
- Click **Create access key**.

## 3. 💾 Save the Access Key
- **Copy the Access Key ID and Secret Access Key** immediately.
- You **will not be able to see the secret again**.
- Optionally, download the credentials as a `.csv` file for safekeeping.

## ✅ Test Your Setup
To verify the credentials are working, run the following in your terminal:

```bash
aws iam get-user

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.
