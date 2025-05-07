A beginner-friendly GitHub repository with clear code examples and step-by-step demos for a Terraform training session.

---

## 🔹 🏗️ What is IaC?
Infrastructure as Code (IaC) is the practice of managing and provisioning cloud or on-prem infrastructure using code instead of manual processes.
Think of IaC as a blueprint for your servers, networks, and configurations! 📜

![IaC](https://k21academy.com/wp-content/uploads/2020/11/Explanation-of-how-IaC-works.jpg)


## ✨ Why use IaC?
- ✅ Repeatable: Same config = same result every time.
-  🚀 Fast: Deploy infrastructure in minutes.
- 🔄 Version-controlled: Use Git to track changes, roll back when needed.
- 🤝 Collaborative: Teams can work together on infrastructure code, just like app code.
-  🔒 Fewer Errors: No manual setup means fewer mistakes.

## 🏆 Final Thoughts
- 🚀 IaC saves time, prevents mistakes, and scales infrastructure easily!
- 🔧 Whether you use Terraform, Ansible, or CloudFormation, IaC is the future of DevOps!
---

## 🔹 1️⃣ Introduction to Terraform & LifeCycle

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
**What This Does**:
This code tells Terraform to generate a random pet name with 2 words like "happy-panda" or "silly-tiger".

Run this:
```sh
terraform init  # Sets up Terraform (downloads provider)
terraform plan  # Shows what will happen
terraform apply # Runs it and gives you a random name
```
---

## 🔹 2️⃣ Terraform Lifecyle
 ![lifecycle](https://k21academy.com/wp-content/uploads/2020/11/terraform-lifecycle.png)

The Terraform Lifecycle typically consists of:
- 1️⃣ Initialization (terraform init) – Sets up Terraform in the working directory.
- 2️⃣ Planning (terraform plan) – Shows proposed changes before applying them.
- 3️⃣ Applying (terraform apply) – Deploys infrastructure changes.
- 4️⃣ Destroying (terraform destroy) – Removes resources when no longer needed


### Terraform init
- `terraform init` is like "setting up the toolbox".
- `Real world` It ensures you have the right plugins, modules, and configurations in place— `just like a carpenter setting up their workstation before building something` & 
   `Another fun example: Think of terraform init as preheating the oven before baking`
- It downloads providers (plugins) and prepares the working directory.
- Creates a `.terraform/` folder.

### 💻 Demo
Create a new folder (e.g., `01-init-provider`), add basic config, and run:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}
```

```sh
terraform init
```
Show:
- `.terraform/` directory
- Plugin downloads

--- 
## 🔹 2️⃣ Terraform Installation
 [tf-installation-guide](https://github.com/amir-projects/tf-installation-guide)
## 🔹 3️⃣ Terraform Providers
  ![Providers](https://k21academy.com/wp-content/uploads/2020/11/Terraform-provider-api-call.png)

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

## 🔚 Q&A + Recap

### 🎯 Key Takeaways:
- Terraform = Powerful tool to manage cloud infra
- Flow: `write → init → plan → apply → update`
- Just `.tf` files + Terraform CLI = good to go

---

## 🌱 What’s Next?
- variables,outputs,dynamic blocks, fmt,imports

---

## ✅ What You’ll Need for Demo
- Terraform CLI installed
- VSCode or your favorite editor
- AWS CLI configured (use dummy/learning account)
- Internet connection to download providers

---

> 📁 Each folder (`00-` to `03-`) in this repo has self-contained `.tf` files and guides.

Happy Terraforming! 💻☁️
Feel free to reach out shohag_ict@live.com

