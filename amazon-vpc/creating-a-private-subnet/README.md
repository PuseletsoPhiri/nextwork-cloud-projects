<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Creating a Private Subnet

**Project Link:** [View Project](https://nextwork.ai/projects/4e96e29d-98b8-551e-ae93-da39c36e30fd)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create a private subnet in an AWS VPC. I'm doing this project to learn how to isolate sensitive resources like databases from public internet access using private subnets, dedicated route tables, and restrictive network ACLs.

### ✍️ What are we doing in this step?

In this step, I will set up the foundational AWS networking resources, including a VPC, subnets, an internet gateway, a route table, a security group, and a network ACL because these components form the backbone of our cloud environment and are required before we can create the private subnet.

### ✍️ What are we doing in this step?

In this step, I will create a private subnet with its own unique CIDR block (10.0.1.0/24) because it keeps sensitive resources like databases isolated from the public internet while avoiding IP address conflicts with the existing public subnet.

### What is Amazon VPC?

Amazon VPC is a virtual network isolated in the AWS cloud. It is useful because you get full control over your own network settings like IP ranges and security rules, to keep your resources safe and organized.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a private subnet with its own route table and network ACL. This keeps sensitive resources like databases isolated from the public internet, just like a locked back room in a shop that only staff can enter.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is that AWS blocks duplicate CIDR blocks with an error, forcing each subnet to have its own unique IP range, like separate street addresses.

### This project took me...

This project took me about 30 minutes, including documentation

## Private vs Public Subnets

The difference between public and private subnets is that a public subnet has direct internet access via an internet gateway, while a private subnet does not and keeps resources hidden from the public internet.

Having private subnets is useful because they keep sensitive resources like databases hidden from the public internet, so only trusted resources inside your VPC (like your web server in the public subnet) can reach them. e.g., it is like a shop: the front counter is open to customers, but the safe with cash and records stays in a back room only staff can enter.

My private and public subnets cannot have the same CIDR block. Each subnet needs a unique IP range, like two houses can't share the same street address.

### ✍️ What are we doing in this step?

In this step, I will create a private route table because it stops traffic from reaching the internet and keeps my private subnet isolated from public access.

![Private vs Public Subnets](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_afe1fdbd)

## A dedicated route table

By default, my private subnet is associated with the default route table for the VPC.

I had to set up a new route table because the existing one has a route to an internet gateway, which would make my subnet public. A dedicated private route table keeps traffic inside the VPC and blocks direct internet access.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows traffic to stay within the VPC local network.

### ✍️ What are we doing in this step?

In this step, I will create a private network ACL because the default ACL allows all traffic, which leaves my private subnet exposed if any part of my VPC gets compromised.

![A dedicated route table](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_b4b904b5)

## A new network ACL

By default, my private subnet is associated with the default network ACL for the VPC. Think of this as the VPC's "open gate" policy that allows all traffic by default. I replaced this with a custom private NACL to lock things down and only allow specific trusted traffic.

I set up a dedicated network ACL for my private subnet because the default one acts like an open gate allowing all traffic. The new NACL works like a bouncer at a club door, checking IDs to only let trusted traffic in while keeping the sensitive data safe inside.

My new network ACL has two simple rules that deny all inbound and outbound traffic by default.

![A new network ACL](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/4e96e29d-98b8-551e-ae93-da39c36e30fd_1ed2cb07)
