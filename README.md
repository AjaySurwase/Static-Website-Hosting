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

5. Then below command for creating the bucket :

   ```hcl
       terraform apply -auto-approve
   ```
   
6. And then add the below codes in main.tf file :

```
resource "aws_s3_bucket" "bucket1" {
  bucket = "web-bucket-ajay"

}
resource "aws_s3_bucket_public_access_block" "bucket1" {
  bucket = aws_s3_bucket.bucket1.id

  block_public_acls       = false
  block_public_policy     = false
  ignore_public_acls      = false
  restrict_public_buckets = false
}

resource "aws_s3_object" "index" {
  bucket       = "web-bucket-ajay"
  key          = "index.html"
  source       = "index.html"
  content_type = "text/html"
}

resource "aws_s3_object" "error" {
  bucket       = "web-bucket-ajay"
  key          = "error.html"
  source       = "error.html"
  content_type = "text/html"
}


resource "aws_s3_bucket_website_configuration" "bucket1" {
  bucket = aws_s3_bucket.bucket1.id

  index_document {
    suffix = "index.html"
  }

  error_document {
    key = "error.html"
  }

}

resource "aws_s3_bucket_policy" "public_read_access" {
  bucket = aws_s3_bucket.bucket1.id
  policy = <<EOF
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
	  "Principal": "*",
      "Action": [ "s3:GetObject" ],
      "Resource": [
        "${aws_s3_bucket.bucket1.arn}",
        "${aws_s3_bucket.bucket1.arn}/*"
      ]
    }
  ]
}
EOF
}

```

7. And then again run the command :

```
terraform applyb -auto-approve
```
8. The code above will apply the necessary configurations for features such as static website hosting, bucket policies, and blocking public access to your bucket.
9. Certainly, it's important to customize the code to your specific needs. Please remember to change the bucket name, region, and configurations as per your requirements when using the code from the Terraform documentation.

### Step 5: Define the Output file

1. We use an output file to obtain your website link in your IDE, eliminating the need to access the link through the AWS Console.
2. Define __output.tf__ file by using the below terraform code :
```
output "website_endpoint" {
  value = aws_s3_bucket_website_configuration.bucket1.website_endpoint
}

```
3. And then run the following command :

```
terraform apply -auto-approve
```
4. It will give your website link as output as shown below

![image](https://github.com/user-attachments/assets/4ae382c2-7c7e-4f68-8d5d-d50919bb6aa5)

### Step 6: Verify the Output 

Copy the link and paste it in your favourite browser.

![image](https://github.com/user-attachments/assets/4da00601-76a0-4cbc-a0e9-dc555b2bac74)



