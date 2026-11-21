<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Access S3 from a VPC

**Project Link:** [View Project](https://nextwork.ai/projects/36d7dc8f-3a9f-51ff-91ae-662077ea9920)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to let resources inside a VPC talk to AWS services that live outside it, using Amazon S3 as the example. I'll set up a VPC with an EC2 instance in a public subnet, create IAM access keys, configure the AWS CLI on the instance, then list buckets and upload a file into S3 from the instance's terminal.

I'm doing this project to learn how credentials work outside the AWS Console, why an EC2 instance needs its own "username and password" (access key ID plus secret access key) to call AWS APIs, and how the AWS CLI becomes the everyday tool for managing cloud resources. It also sets me up for the next project, where I'll replace public-internet traffic with a VPC endpoint for private, cheaper, more secure access to S3.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you can launch resources in a virtual network that you define. It is useful because it gives you full control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a private network where my EC2 instance lives. This gave me a secure place to launch resources and test how they reach AWS services outside the VPC, like S3.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easy it was to manage AWS services from the terminal. Using the AWS CLI felt like having a direct remote control for my account instead of clicking through the console.

### This project took me...

This project took me 1 hour, including documentation.

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will create a VPC from scratch (10.0.0.0/16, 1 AZ, 1 public subnet, no NAT gateway or endpoints) and launch a t3. micro EC2 instance into its public subnet with a public IP and a security group allowing SSH.

I'm doing this because the VPC is the private network my resources live in, and the EC2 instance is the machine that will later run AWS CLI commands to reach S3. Without both set up, there's nothing inside the VPC to test access with.

### Step 2 - Connect to my EC2 instance

In this step, I will connect to my EC2 instance using EC2 Instance Connect and run the \`aws s3 ls\` command to list S3 buckets. I'm doing this because I need to test if my instance can access AWS services. Running the command without credentials will show that access keys are required, which sets up the next step where I create those keys.

### Step 3 - Set up access keys

In this step, I will create IAM access keys for my account and save them securely. I'm doing this because my EC2 instance needs its own credentials to identify itself and securely access AWS services like S3.

## Architecture set up

I started my project by launching a VPC with a single public subnet and one t3.micro EC2 instance running Amazon Linux 2023. I also created a security group that allows SSH access so I can connect to the instance using EC2 Instance Connect.

I also set up an S3 bucket named \`nextwork-vpc-project-puseletso\` and uploaded two files into it. This gives my EC2 instance a real target to practice listing and interacting with objects.

![Architecture set up](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d777)

## Running CLI commands

AWS CLI is like a remote control for your AWS account. Instead of clicking buttons in the browser, you type commands to manage services. I have access to AWS CLI because it comes pre-installed on my EC2 instance. This lets me control AWS services directly from the terminal.

The second command I ran was aws configure. This command is used to save my AWS credentials (access key ID and secret access key), region, and output format so the CLI knows who I am and which account to talk to.

![Running CLI commands](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_e7fa8776)

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured the AWS CLI with my access key ID, secret access key, region, and output format. This allows my instance to securely communicate with AWS services like S3.

Access keys are the credentials that let your EC2 instance (or any application) securely access and manage AWS services. They come in a pair: an access key ID (like a username) and a secret access key (like a password). Both are needed together to authenticate API calls made through the AWS CLI.

Secret access keys are the password half of an AWS access key pair. They stay private and prove your identity when you call AWS services. Anyone who has one can act as you in your account, so never share or commit it to code.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM role attached to the EC2 instance. The instance inherits the role's permissions automatically, so no long-lived secrets sit on the machine, and you can grant or revoke access instantly by attaching or detaching the role.

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will create an S3 bucket and upload two files into it. I'm doing this because I need a real bucket with objects inside it so my EC2 instance has something to list and interact with once the access keys are configured.

### Step 5 - Connecting to my S3 bucket

In this step, I will configure the AWS CLI with my access keys and run commands to list my S3 buckets and upload a test file from my EC2 instance to my S3 bucket. I'm doing this because I need to verify that my EC2 instance can successfully access and manage my S3 resources using the credentials I created.

## Connecting to my S3 bucket

The first command I ran was \`aws s3 ls\`. This command is used to list all the S3 buckets in my account. It is like looking at a list of folders.

When I ran the command aws s3 ls again, the terminal responded with a list of my account's S3 buckets, including nextwork-vpc-project-puseletso. This indicated that my access keys worked and my EC2 instance could now securely reach S3 through the AWS CLI.

![Connecting to my S3 bucket](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d778)

## Connecting to my S3 bucket

Another CLI command I ran was \`aws s3 ls s3://nextwork-vpc-project-puseletso\`, which returned the list of files (objects) inside that specific bucket.

![Connecting to my S3 bucket](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_4334d779)

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command \`sudo touch /tmp/test.txt\`. This command creates an empty text file named test.txt in the temporary directory.

The second command I ran was \`aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-puseletso\`. This command will copy the test.txt file from my EC2 instance and upload it into my S3 bucket.

The third command I ran was \`aws s3 ls s3://nextwork-vpc-project-puseletso\`, which validated that my new test.txt file was successfully uploaded and now lives inside the bucket.

![Uploading objects to S3](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/36d7dc8f-3a9f-51ff-91ae-662077ea9920_3e1e79a2)
