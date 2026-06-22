## Connecting to AWS EC2 & Automating Virtual Machine Creation

---

# 1. Connecting to an AWS EC2 Instance

## Method 1: AWS Console (Web UI)

Steps:

1. Open AWS Console.
2. Go to **EC2 Dashboard**.
3. Select the running instance.
4. Click the **Instance ID**.
5. Click **Connect**.
6. Click **Connect** again.

You will get a browser-based terminal connected to the EC2 instance.

Example commands:

```bash
touch Dummyfile                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
ls
```

This creates a file and verifies access.

### Drawbacks

* Not efficient for DevOps work.
* Must log in through AWS Console every time.
* Sessions can expire.
* Difficult when managing many servers.

---

# 2. Preferred Method: Terminal Access Using SSH

DevOps engineers usually use local terminals.

### Terminal Options

### Mac

* iTerm2 (recommended)

### Windows

* PuTTY
* MobaXterm (recommended)
* NoMachine

---

# 3. Connecting via SSH

Use the instance's **Public IP Address**.

Do NOT use:

```text
Private IP
```

because private IPs are only accessible inside AWS networking.

### Basic SSH Command

```bash
ssh ubuntu@PUBLIC_IP
```

This will fail because authentication is missing.

---

# 4. Using PEM Key Authentication

Use:

```bash
ssh -i key.pem ubuntu@PUBLIC_IP
```

Where:

* `-i` = identity file
* `key.pem` = downloaded key pair

---

# 5. Fixing PEM File Permissions

If permissions are too open:

```bash
chmod 600 key.pem
```

Meaning:

* Owner = Read + Write
* Others = No access

Then reconnect:

```bash
ssh -i key.pem ubuntu@PUBLIC_IP
```

Successful login:

```bash
ls
touch Dummyfile
ls
```

---

# 6. Managing EC2 Instances

### Stop Instance

Used when:

* Temporarily not needed
* Want to reduce costs

### Terminate Instance

Used when:

* Instance is no longer required
* Permanently deletes the server

Best practice:

```text
Stop → Verify → Terminate
```

---

# 7. AWS CLI (Command Line Interface)

AWS CLI allows interaction with AWS services directly from the terminal.

---

## Installing AWS CLI

Download from AWS documentation.

Available for:

* Windows
* Mac
* Linux

Verify installation:

```bash
aws --version
```

Example output:

```bash
aws-cli/2.x.x
```

---

# 8. AWS Authentication

AWS CLI alone is not enough.

You must authenticate.

---

## Creating Access Keys

AWS Console:

```text
Profile
→ Security Credentials
→ Access Keys
→ Create Access Key
```

You receive:

* Access Key ID
* Secret Access Key

⚠️ Never share these keys.

---

# 9. Configure AWS CLI

Run:

```bash
aws configure
```

Provide:

```text
AWS Access Key ID
AWS Secret Access Key
Default Region
Output Format (JSON)
```

Example:

```bash
aws configure
```

Input:

```text
Access Key ID: XXXXX
Secret Access Key: XXXXX
Region: us-east-1
Output: json
```

---

# 10. Testing AWS CLI

List S3 buckets:

```bash
aws s3 ls
```

Output:

```text
bucket1
bucket2
bucket3
```

Shows AWS CLI is connected successfully.

---

# 11. Creating AWS Resources Using CLI

Example EC2 creation command:

```bash
aws ec2 run-instances
```

Requires:

* AMI ID
* Instance Type
* Key Pair
* Security Group
* Subnet ID

AWS Documentation provides all required options.

---

# 12. AWS CloudFormation Templates (CFT)

CloudFormation is Infrastructure as Code (IaC).

Instead of clicking buttons manually:

* Write a template
* AWS creates resources automatically

Workflow:

```text
Template
→ CloudFormation Stack
→ AWS Resources
```

---

## Using CloudFormation

1. Open AWS CloudFormation.
2. Create Stack.
3. Upload template.
4. Launch stack.

Templates can be found from:

* AWS Examples
* GitHub repositories

---

# 13. Infrastructure as Code (IaC)

CloudFormation belongs to IaC.

Other IaC tools:

* Terraform
* AWS CDK
* CloudFormation

Detailed learning will happen later in the course.

---

# 14. AWS API Automation

AWS can be automated using programming languages.

Examples:

* Python
* Shell Scripts
* Java
* Go

---

# 15. Boto3 (Python AWS SDK)

Most common Python library for AWS:

```python
import boto3
```

Boto3 allows:

* Creating EC2 instances
* Listing EC2 instances
* Creating S3 buckets
* Managing AWS resources

---

## Installing Boto3

```bash
pip install boto3
```

---

## Authentication

Boto3 automatically uses credentials from:

```bash
aws configure
```

configuration files.

No need to repeatedly enter credentials.

---

# 16. Ways to Create AWS Resources

| Method         | Description            |
| -------------- | ---------------------- |
| AWS Console    | Manual UI              |
| AWS CLI        | Command Line           |
| CloudFormation | Infrastructure as Code |
| Boto3          | Python Automation      |
| AWS API        | Direct API Calls       |
| Terraform      | Infrastructure as Code |

---

# Assignment

### 1. Install AWS CLI

Verify:

```bash
aws --version
```

---

### 2. Create AWS Access Keys

AWS Console:

```text
Security Credentials
→ Access Keys
```

---

### 3. Configure AWS CLI

```bash
aws configure
```

---

### 4. Test AWS Connection

List S3 buckets:

```bash
aws s3 ls
```

OR

List EC2 instances:

```bash
aws ec2 describe-instances
```

---

### 5. Explore AWS CLI Documentation

Look up:

* S3 commands
* EC2 commands
* IAM commands

Documentation contains examples for almost every AWS service.

---

# Key Takeaways for Interviews

1. EC2 instances can be accessed through AWS Console or SSH.
2. SSH requires a PEM key and proper permissions (`chmod 600`).
3. AWS CLI is the easiest automation tool for beginners.
4. `aws configure` is required before using AWS CLI.
5. Access Key ID and Secret Access Key authenticate AWS users.
6. CloudFormation and Terraform are Infrastructure as Code (IaC) tools.
7. Boto3 is the Python SDK used to automate AWS operations.
8. DevOps engineers prefer automation over manual AWS Console operations.
