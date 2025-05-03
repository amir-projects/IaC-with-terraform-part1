# Terraform Basics: Hands-On Workshop

A beginner-friendly GitHub repository with clear code examples and step-by-step demos for a Terraform training session.

---

## 🔹 1️⃣ Introduction to Terraform & Core Concepts

### 🎙️ Easy Explanation
**What is Terraform?**
> "A tool that builds and manages your cloud infrastructure using simple files."

**What does it do?**
- Automates creating servers, databases, networks, etc.
- Like writing a recipe for cloud resources.

**Core idea:**
> "You write what you want → Terraform builds it → You change the file → Terraform updates it."

### 💻 Demo
#### `00-random-pet/main.tf`
```hcl
resource "random_pet" "name" {
  length = 2
}
```
Run this:
```sh
terraform init
terraform plan
terraform apply
```

---

## 🔹 2️⃣ Terraform Init

### 🎙️ Easy Explanation
- `terraform init` is like "setting up the toolbox".
- It downloads providers (plugins) and prepares the working directory.
- Creates a `.terraform/` folder.

### 💻 Demo
Create a new folder (e.g., `01-init-provider`), add basic config, and run:
```sh
terraform init
```
Show:
- `.terraform/` directory
- Plugin downloads

---

## 🔹 3️⃣ Terraform Providers

### 🎙️ Easy Explanation
- **Providers** are plugins that tell Terraform how to talk to cloud platforms.
- Example: AWS, GCP, Azure, etc.

**Without providers, Terraform can't do anything.**

### 💻 Demo
#### `02-aws-provider/main.tf`
```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "demo" {
  ami           = "ami-0c55b159cbfafe1f0" # dummy, won’t launch
  instance_type = "t2.micro"
  count         = 0
}
```
> ⚠️ Use `count = 0` to avoid charges.

**Best Practice:**
- Avoid hardcoded credentials.
- Use `aws configure` or environment variables.

---

## 🔹 4️⃣ Terraform State

### 🎙️ Easy Explanation
- Terraform keeps a **state file** to track what it built.
- Avoids rebuilding existing resources.

### 💻 Demo
#### `03-state-demo/main.tf`
```hcl
resource "random_pet" "state_test" {
  length = 2
}
```
Run:
```sh
terraform apply
terraform state list
terraform state show random_pet.state_test
```
Edit `length = 3` and rerun `terraform plan`.

---

## 🔹 5️⃣ Variables and Outputs

### 🎙️ Easy Explanation
- **Variables** = Make code configurable.
- **Outputs** = Return useful values after apply.

### 💻 Demo
#### `02-aws-provider/variables.tf`
```hcl
variable "region" {
  default = "us-west-2"
}
```
Update provider block:
```hcl
provider "aws" {
  region = var.region
}
```
Create `outputs.tf`:
```hcl
output "bucket_arn" {
  value = aws_s3_bucket.demo.arn
}
```
Use:
```sh
tfvars or -var="region=us-west-2"
```

---

## 🔚 Q&A + Recap

### 🎯 Key Takeaways:
- Terraform = Powerful tool to manage cloud infra
- Flow: `write → init → plan → apply → update`
- Just `.tf` files + Terraform CLI = good to go

---

## 🌱 What’s Next?
- Try launching an EC2 or S3 bucket
- Learn about modules, remote state, Terraform Cloud

---

## ✅ What You’ll Need for Demo
- Terraform CLI installed
- VSCode or your favorite editor
- AWS CLI configured (use dummy/learning account)
- Internet connection to download providers

---

> 📁 Each folder (`00-` to `03-`) in this repo has self-contained `.tf` files and guides.

Happy Terraforming! 💻☁️
