<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# VPC Endpoints

**Project Link:** [View Project](https://nextwork.ai/projects/749fab76-0a0b-5822-9b31-c7863050c9bd)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create a VPC endpoint (S3 Gateway type) that lets my EC2 instance talk to an S3 bucket privately, without traffic going over the public internet. I'm doing this project to learn how to set up a VPC endpoint, lock down an S3 bucket with a strict bucket policy that only allows traffic from that endpoint, and fix routing issues by adding the endpoint route to my subnet's route table.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you can launch resources in a virtual network that you define. It is useful because it gives you full control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to host my EC2 instance and connect it privately to S3 through a gateway endpoint. The route table in my VPC directed all S3 traffic through that endpoint instead of the internet gateway, keeping my data inside the AWS network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how a single missing route table entry could break my entire endpoint setup. It felt like building a perfect private tunnel but forgetting to put up the sign telling traffic where to turn.

### This project took me...

This project took me an hour and 30 minutes, including doccumentation

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will set up the foundation by creating a VPC, launching an EC2 instance, and setting up an S3 bucket because I need these three core resources in place before I can connect them or configure any networking rules.

### Step 2 - Connect to EC2 instance

In this step, I will connect to my EC2 instance using EC2 Instance Connect and check if I can access S3 buckets because I need to test the current setup before creating the VPC endpoint. This helps me see what happens when traffic goes through the public internet so I can compare it with the secure endpoint connection later.

### Step 3 - Set up access keys

In this step, I will create access keys for my IAM user because my EC2 instance needs a username and password to talk to AWS services. Without these keys the AWS CLI commands will fail with permission errors.

### Step 4 - Interact with S3 bucket

In this step, I will configure AWS CLI with my access keys and run commands to list, upload and manage files in my S3 bucket because I need to prove my EC2 instance can reach S3 through the public internet before we set up the private endpoint. This gives me a baseline to compare against the secure connection later.

## Architecture set up

I started my project by launching a VPC called NextWork (with one public subnet and no NAT gateway) and an EC2 instance named Instance - NextWork VPC Project running Amazon Linux 2023 on t3. micro with a security group called SG - NextWork VPC Project.

I also set up an S3 bucket named nextwork-vpc-project-puseletso with two image files uploaded into it.

![Architecture set up](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d777)

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured my access key ID, AWS secret access key, default region name, and default output format. These are the four pieces of info AWS CLI needs to know who I am, where I am, and how I want results displayed.

Access keys are like a username and password for your EC2 instance. They let it securely log into AWS to access services like S3.

Secret access keys are the password half of your credentials. They pair with your access key ID (the username) to prove who you are when talking to AWS. Keep them private because anyone who has one can access your account.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use an IAM role attached directly to the EC2 instance. This is like giving your instance a permanent company badge instead of a temporary login card. The instance automatically inherits the permissions from the role, so you do not need to manage or rotate any keys manually. It is much more secure and easier to maintain.

## Connecting to my S3 bucket

The command I ran was \`aws s3 ls\`. This command is used to list all the S3 buckets in my AWS account. It helps me see what buckets exist and confirms my AWS CLI is working properly.

The terminal responded with a list of my account's S3 buckets, including nextwork-vpc-project-puseletso. This indicated that the access keys I set up were working correctly, and my EC2 instance could now reach S3 through the public internet.

![Connecting to my S3 bucket](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d778)

## Connecting to my S3 bucket

I also tested the command \`aws s3 ls s3://nextwork-vpc-project-puseletso\` which returned a list of the files inside my bucket.

![Connecting to my S3 bucket](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4334d779)

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command \`sudo touch /tmp/nextwork.txt\`. This command creates an empty text file called nextwork.txt inside the temporary folder on my EC2 instance. Think of it like opening a blank document before you can save it somewhere else.

The second command I ran was \`aws s3 cp /tmp/nextwork.txt s3://nextwork-vpc-project-puseletso\`. This command will copy the empty file from my EC2 instance and upload it straight into my S3 bucket, like moving a document from your desktop into a cloud folder.

The third command I ran was \`aws s3 ls s3://nextwork-vpc-project-puseletso\` again, which validated that my file upload worked because nextwork.txt now showed up in the bucket listing with a size of 0 bytes.

![Uploading objects to S3](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_3e1e79a2)

## In the second part of my project...

### Step 5 - Set up a Gateway

In this step, I will create a VPC endpoint of type 'Gateway' for S3 because I need to build a private highway between my VPC and S3. This lets traffic flow directly through AWS networks instead of going out to the public internet, where it could be intercepted.

### Step 6 - Bucket policies

In this step, I will create a strict bucket policy that blocks all access to my S3 bucket except traffic coming from my VPC endpoint because I need to prove my endpoint is truly working. If my EC2 instance can still reach the bucket after I lock everything else out, then my private connection is set up correctly.

### Step 7 - Update route tables

In this step, I will test my VPC endpoint setup by running \`aws s3 ls\` again and troubleshoot any connectivity issues because I need to confirm whether my EC2 instance can still reach the bucket through the private endpoint after locking down all other access. If it fails, I have to find and fix what's blocking the traffic.

![In the second part of my project...](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_67081648)

### Step 8 - Validate endpoint conection

In this step, I will run \`aws s3 ls\` again to confirm access works through the endpoint, then edit the endpoint policy to Deny and watch access break because I need to prove the endpoint is doing the work, and show that endpoint policies give me an instant kill switch on access if something goes wrong.

## Setting up a Gateway

I set up an S3 Gateway, which is a type of VPC endpoint that acts like a private bridge to S3. It works by adding a route to your subnet's route table so traffic going to S3 heads straight to the endpoint instead of the internet. e.g. it acts as a dedicated toll road that bypasses all the public traffic jams

### What are endpoints?

An endpoint is a private door inside AWS that connects your VPC directly to services like S3, so traffic never touches the public internet. e.g., it acts as a secure tunnel between your building and the warehouse instead of sending packages through the open road.

![Setting up a Gateway](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_09bcaa8a)

## Bucket policies

A bucket policy is a rulebook for your S3 bucket that says who can access it and what they can do. e.g. it acts like a security guard at your building who only lets people with the right badge through the door.

My bucket policy will deny all access to my S3 bucket for everyone except traffic coming from my specific VPC endpoint. It acts like a bouncer that only lets people through a secret back door while keeping the front entrance locked.

![Bucket policies](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_7316a13d)

## Bucket policies

Right after saving my bucket policy, my S3 bucket page showed 'denied access' warnings. This was because the policy blocks everyone except traffic from my VPC endpoint, and the AWS Console is not going through that endpoint. Think of it like locking every door in your house but only leaving the garage open. The front door (the console) now gets turned away.

I also had to update my route table because my public subnet had no route pointing S3 traffic to my VPC endpoint. Without that route, my EC2 instance was still sending requests out through the internet gateway instead of the private endpoint, so the bucket policy blocked it. Adding the route is like telling your GPS to use the private tunnel rather than the public road.

![Bucket policies](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_4ec7821f)

## Route table updates

To update my route table, I went to the VPC Endpoints page, selected my endpoint, clicked "Manage route tables", selected the checkbox next to my public route table, and then clicked "Modify route tables" to add the endpoint route. This is like adding a new signpost on the highway telling all S3 traffic to take the private exit instead of the public road.

After updating my public subnet's route table, my terminal could return a successful list of files inside my S3 bucket. This proved my EC2 instance was now reaching S3 through the private VPC endpoint instead of the public internet.

![Route table updates](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_d116818e)

## Endpoint policies

An endpoint policy is a rule attached to your VPC endpoint that controls what traffic can pass through it. It acts like a gatekeeper on the private tunnel, letting you instantly block or allow access to AWS services without touching the service itself.

I updated my endpoint's policy by switching "Effect": "Allow" to "Effect": "Deny". I could see the effect of this right away, because \`aws s3 ls\` instantly failed with Access Denied. Flipping one line closed the gate on the private tunnel and cut off all S3 access.

![Endpoint policies](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/749fab76-0a0b-5822-9b31-c7863050c9bd_3e1e79a3)
