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

## Notes
- Ensure your AWS and Azure credentials are properly configured before running Terraform.
- Always review the Terraform plan output before applying changes.
- Use caution when modifying or destroying cloud resources.
- Be sure to manually clean up AWS and Azure environments if you lose your terraform tfstate file. Also, check for any duplicates created if you encounter errors to keep your Cloud Costs down.

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.
