# Static-Website-Hosting
Static Website Hosting(Terraform)
Terraform AWS S3 Static Website Hosting

**Project Description:**
This project demonstrates how to set up a static website hosting infrastructure using Terraform and Amazon Web Services (AWS) S3. The goal is to automate the provisioning and deployment of a static website using Infrastructure as Code (IaC).

**Overview:**
The project uses AWS S3 to host a static website. Terraform automates the creation and management of the necessary resources.
![image](https://github.com/user-attachments/assets/b2221dc6-509f-4bd1-8da5-1badf221259a)

**Key Components and Features:**

**Terraform (IaC):**
Terraform is used to define and provision the AWS resources needed for the static website hosting. This allows for version control and repeatable deployments.

**AWS S3 Bucket:**
An S3 bucket is created to store and serve the static website files, configured for website hosting to ensure easy content delivery.

**Content Management:**
Scripts and instructions are provided for uploading and managing the website content in the S3 bucket.

**Prerequisites:**
1. Basic knowledge of AWS services and concepts.
2. Familiarity with Terraform and infrastructure as code principles.
3. An AWS account with appropriate permissions.
4. An IDE of your Choice , I would suggest VS Code Editor .
5. This project serves as an excellent foundation for hosting various types of static websites, including personal blogs, portfolio sites, or small business websites.

**Step 1: Set Up Your Development Environment**
Install Terraform and the AWS Command Line Interface (CLI) on your local machine. Configure your AWS credentials by running aws configure and providing your AWS access key and secret key.

**Step 2: Define Your Website Content**
To prepare static website files (HTML), place them in the directory where your Terraform configuration files are located. Name the main HTML file "index.html," and optionally, you can also include an "error.html" file. If you prefer, you can reference my repository for the static website HTML files.

**Step 3: Terraform Configuration File Syntax**
If we want to Create a terraform configuration file we have to use .tf (e.g., main.tf) to define the infrastructure as code using terraform.

**Step 4: Define your Configuration Files in your IDE**
Define the AWS provider and required resources like S3 buckets, IAM roles, and policies
1. Define provider.tf file using the below code :
    ```hcl
        provider "aws" {
            region = "ap-south-1"
        }
    ```
2. In your Integrated Development Environment (IDE), open the terminal and navigate to the directory where you have created these configuration files.
3. After navigating to the directory where your configuration files are located in your IDE's terminal, you can run the following command to initialize Terraform and prepare it for use with AWS:

   ```hcl
       terraform init
   ```
Running `terraform init` will install the necessary plugins and modules required for connecting to AWS and managing your infrastructure.
4. And then define resource.tf file for creating bucket by using the below code :
    ```hcl
        resource "aws_s3_bucket" "bucket1" {
            bucket = "web-bucket-ajay"
        }
    ```
