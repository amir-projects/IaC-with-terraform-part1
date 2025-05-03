# Terraform Basics Demo Repository

This repository contains beginner-friendly Terraform demo projects for a 1.5-hour hands-on session. Each folder focuses on a single concept with simple `.tf` files and step-by-step guides.

## 🚀 Getting Started
Ensure you have the following installed:
- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- AWS credentials configured using `aws configure`

---

## 📁 00-random-pet
### 📄 main.tf
```hcl
resource "random_pet" "name" {
  length = 2
}
```
### ✅ Steps
```sh
terraform init
terraform plan
terraform apply
```
This shows a basic resource without any cloud provider.

---

## 📁 01-init-provider
### 📄 main.tf
```hcl
terraform {
  required_providers {
    random = {
      source = "hashicorp/random"
    }
  }
}

provider "random" {}

resource "random_pet" "name" {
  length = 2
}
```
### ✅ Steps
```sh
terraform init
terraform apply
```
Demonstrates how providers are downloaded and initialized.

---

## 📁 02-aws-provider
### 📄 main.tf
```hcl
provider "aws" {
  region = var.region
}

resource "aws_s3_bucket" "demo" {
  bucket = var.bucket_name
  acl    = "private"
}
```

### 📄 variables.tf
```hcl
variable "region" {
  default = "us-east-1"
}

variable "bucket_name" {}
```

### 📄 outputs.tf
```hcl
output "bucket_arn" {
  value = aws_s3_bucket.demo.arn
}
```

### 📄 terraform.tfvars
```hcl
bucket_name = "my-demo-terraform-bucket-123"
```

### ✅ Steps
```sh
terraform init
terraform plan
terraform apply
```
Shows a real cloud resource creation using AWS provider with variables & outputs.

---

## 📁 03-state-demo
### 📄 main.tf
```hcl
resource "random_pet" "state_test" {
  length = 2
}
```
### ✅ Steps
```sh
terraform apply
terraform state list
terraform state show random_pet.state_test
```
Then change `length = 2` to `length = 3` and rerun `terraform plan` to observe state tracking.

---

## 🧠 Key Concepts Covered
- Terraform Init
- Terraform Providers
- Terraform State
- Variables and Outputs

---

## 📘 Next Steps
- Try adding another resource (like an EC2 instance)
- Learn about modules and remote state
- Explore [Terraform Registry](https://registry.terraform.io/)

---

Happy Terraforming! 🌍

---
> Need help? Raise an issue or reach out!

