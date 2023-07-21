# Cloud Developer using AWS - Udacity - Project 01 - Deploy Static Website to AWS S3

- [Cloud Developer using AWS - Udacity - Project 01 - Deploy Static Website to AWS S3](#cloud-developer-using-aws---udacity---project-01---deploy-static-website-to-aws-s3)
  - [Project Overview](#project-overview)
  - [Installation](#installation)
    - [Clone the repository](#clone-the-repository)
    - [AWS CLI Configuration](#aws-cli-configuration)
    - [Terraform](#terraform)
    - [Upload files to AWS S3](#upload-files-to-aws-s3)
    - [Browse the website](#browse-the-website)

## Project Overview

The cloud is perfect for hosting static websites that only include HTML, CSS, and JavaScript files that require no server-side processing. The whole project has two major intentions to implement:

Hosting a static website on S3 and
Accessing the cached website pages using CloudFront content delivery network (CDN) service. Recall that CloudFront offers low latency and high transfer speeds during website rendering.
Note that Static website hosting essentially requires a public bucket, whereas the CloudFront can work with public and private buckets.

In this project, you will deploy a static website to AWS by performing the following steps:

You will create a public S3 bucket and upload the website files to your bucket.
You will configure the bucket for website hosting and secure it using IAM policies.
You will speed up content delivery using AWS’s content distribution network service, CloudFront.
You will access your website in a browser using the unique CloudFront endpoint.

1. Dependencies:

   - [AWS account](https://aws.amazon.com/)
   - [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
   - [Terraform](https://developer.hashicorp.com/terraform/downloads?product_intent=terraform)
   - [Visual Studio Code](https://code.visualstudio.com/)

2. Topics Covered:
   - S3 bucket creation
   - S3 bucket configuration
   - Website distribution via CloudFront
   - Access website via web browser

## Installation

### Clone the repository

Run code to clone the repository

```bash
git clone https://github.com/aws-cloud-dev-udacity-prj1-static-web.git
```

### AWS CLI Configuration

1. Check aws version
   ```bash
   which aws
   # display /usr/local/bin/aws on mac
   aws --version
   # aws-cli/2.10.0 Python/3.11.2 Darwin/18.7.0 botocore/2.4.5
   ```
2. AWS Configurations

   ```bash
   aws config
   # AWS Access Key ID: Enter your AWS Access Key ID
   # AWS Secret Access Key: Enter your AWS AWS Secret Access Key
   # Default region name: Enter your Default region name
   # Default output format: Enter json
   ```

3. Set AWS session token
   ```bash
   aws configure set aws_session_token <your-aws-session-token>
   ```

### Terraform

1. Update your configuration in _terraform.tfvars_
   ```
    region      = "us-east-1"
    bucket_name = "aws-dev-udacity-prj1"
    iam_user    = "static-website-user"
   ```
2. Init Terraform
   ```bash
   terraform init
   ```
3. Validate Terraform
   ```bash
   terraform validate
   ```
4. Plan Terraform
   ```bash
   terraform plan -out solution.plan
   ```
5. Apply Terraform
   ```bash
   terraform apply
   ```

### Upload files to AWS S3

1. List AWS S3 buckets to choose
   ```bash
   aws s3api list-buckets
   ```
2. Goto static website directory
   ```bash
   cd udacity-starter-website
   ```
3. Upload index.html
   ```bash
   aws s3api put-object --bucket <your-bucket-name> --key index.html --body index.html
   ```
4. Upload all files to AWS S3
   ```bash
   aws s3 cp vendor/ s3://<your-bucket-name>/vendor/ --recursive
   aws s3 cp css/ s3://<your-bucket-name>/css/ --recursive
   aws s3 cp img/ s3://<your-bucket-name>/img/ --recursive
   ```

### Browse the website

1. Via AWS S3 Url
   http://<your-bucket-name>.s3-website-us-east-1.amazonaws.com/
   <img src="./screenshots/S3_Website_Preview.png">

2. Via AWS CloudFront Distribution URL
   Goto AWS CloudFront => Distributions => Your Distribution => Domain Name
   Example: d1t2o8wyqsdsdstjd.cloudfront.net
   <img src="./screenshots/CloudFront_Distribution_Web.png">
