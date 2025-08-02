# AWS S3 Bucket with Versioning and Encryption

## Introduction
This project provisions an AWS S3 bucket with versioning and AES256 encryption enabled using Terraform.

**Requirements**

- Terraform v1.2+
- AWS CLI configured (IAM user with S3 permissions)
- An S3 bucket name that is globally unique

**Project Structure**

the name of your directory/
│
├── main.tf
├── variables.tf
├── provider.tf
├── outputs.tf
├── README.md

---

### 1. Create a directory and cd to that directory

bash
```
mkdir name of directory
```

```
cd name of directory
```

---


### 2. Create configuration files

a. Create the file **provider.tf** and the code below.

```
provider "aws" {
  region = var.aws_region
}
```

**This sets your AWS region using a variable.**
 

b. Create **variables.tf** and add the codes below.

```
variable "aws_region" {
  description = "AWS region to deploy resources in"
  type        = string
  default     = "us-east-1"
}

variable "bucket_name" {
  description = "Globally unique name for the S3 bucket"
  type        = string
}
```

**We define the region and bucket name here instead of hardcoding.**

<img width="722" height="697" alt="Image" src="https://github.com/user-attachments/assets/c8df7866-c924-46bb-9d81-5bd586aa46bc" />


c. Create main.tf file and the codes below

```
resource "aws_s3_bucket" "this" {
  bucket = var.bucket_name
  force_destroy = true  # Allows automatic deletion of non-empty buckets during destroy

  tags = {
    Name        = var.bucket_name
    Environment = "Dev"
    Owner       = "Gabriel"
  }
}

resource "aws_s3_bucket_versioning" "this" {
  bucket = aws_s3_bucket.this.id

  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "this" {
  bucket = aws_s3_bucket.this.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}

resource "aws_s3_bucket_public_access_block" "this" {
  bucket = aws_s3_bucket.this.id

  block_public_acls   = true
  block_public_policy = true
  ignore_public_acls  = true
  restrict_public_buckets = true
}
```

<img width="720" height="693" alt="Image" src="https://github.com/user-attachments/assets/55b706c2-c0f1-40df-8398-1f1c271abb62" />


**Note**
Creates an S3 bucket with a unique name from variables.tf.
Enables versioning for tracking changes to files.
Enables server-side encryption (SSE) using AES256 (free tier-compatible).
force_destroy = true allows Terraform to delete even if the bucket has files (use with caution).


d. Create outputs.tf file and the codes below

```
output "bucket_name" {
  description = "The name of the S3 bucket"
  value       = aws_s3_bucket.this.bucket
}

output "bucket_arn" {
  description = "The ARN of the S3 bucket"
  value       = aws_s3_bucket.this.arn
}
```

<img width="726" height="709" alt="Image" src="https://github.com/user-attachments/assets/68182c9d-1821-4fcb-af2f-db9976a288f0" />

<img width="718" height="242" alt="Image" src="https://github.com/user-attachments/assets/22a12f4f-013a-4c80-8eeb-814902e7f906" />


**Outputs.tf shows useful info in your terminal after applying the config.**

---

### 3. Run terraform init

```
terraform init
```
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/18bde0f9-a0ac-4bdb-9514-b19e9b5e962b" />


---


### 4. Run terraform validate

```
terraform validate
```

<img width="463" height="113" alt="Image" src="https://github.com/user-attachments/assets/88b7927a-64da-4b3c-9b30-c9fdd90d0bdd" />


---


###. 5. Run terraform plan

```
terraform plan
```
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/6f4ba654-2099-4579-ba9b-ae9bdf053d5a" />

**Note** you will be requested to enter the name of your bucket.

 
---

 
### 6. Run terraform apply

```
terraform apply
```

Type and enter yes when prompted

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/81f554c3-a58d-4b7b-bcba-5867ef5212dd" />

**Note** you will be requested to enter the name of your bucket.

---


### 7. Run terraform state list

```
terraform state list
```

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/a737edc7-2a53-4dfa-89b4-1a11435f4c35" />

---


### 8. Run terraform show

```
terraform
```

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/a737edc7-2a53-4dfa-89b4-1a11435f4c35" />


---


### 9. Destroy Resources

```
terraform destroy
```
type and enter **yes** when prompted

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/b1ec704c-0e36-4206-a171-b252f71034ed" />

<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/bf9b8819-221c-452b-86df-a38ef721c305" />



---


### 10. Optional: Confirm all your work from the console

---

<img width="1018" height="182" alt="Image" src="https://github.com/user-attachments/assets/c8b164f4-5703-43cd-81cd-2e9598d1b7a6" />

<img width="1025" height="395" alt="Image" src="https://github.com/user-attachments/assets/28bb20fe-24f1-4cd7-a2a6-42bf7135bf94" />

![Image](https://github.com/user-attachments/assets/c85ae49c-1cae-4906-bf55-d78bf6b9f6f2)
