<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Launching VPC Resources

**Project Link:** [View Project](https://nextwork.ai/projects/8f49d756-9e51-58c0-856a-e71e54f064ab)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to launch EC2 instances into both a public and a private subnet inside my VPC, configure key pairs and security groups for secure access, and use the AWS "VPC and more" wizard to build an entire VPC setup in minutes. I'm doing this project to learn hands-on EC2 concepts (AMI, instance types, key pairs, SSH) and how to control network traffic between public and private subnets, plus how to visualize VPC architecture with the resource map.

### ✍️ What are we doing in this step?

In this step, I will set up the VPC foundation by creating a VPC, public and private subnets, an internet gateway, route tables, a security group, network ACLs, and the private subnet resources because these components are the building blocks that define my network's layout, control how traffic flows in and out, and secure my resources before I can launch any EC2 instances into them.

### ✍️ What are we doing in this step?

In this step, I will launch a public EC2 instance, configure a key pair for secure login access, and place the instance in my VPC’s public subnet because I need a live server in a public subnet to test connectivity and demonstrate how resources connect to the internet.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you launch resources in a virtual network you define. It is useful because it gives you full control over your network environment, like choosing IP addresses and setting security rules, while keeping your data secure and separate from other AWS customers.

### How I used Amazon VPC in this project

I used Amazon VPC to launch public and private servers and connect them securely. This let me test how traffic flows between a public internet-facing server and a private server that only accepts requests from within the network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that two VPCs can share the same CIDR block without conflict, because AWS keeps them completely isolated from each other.

### This project took me...

This project took me about 1 hour, including documentation

## Setting Up Direct VM Access

Directly accessing a virtual machine means logging into the server’s operating system over the internet. It lets you run commands, install software, and fix issues just like you were sitting in front of the computer.

### SSH is a key method for directly accessing a VM

SSH traffic means Secure Shell, the protocol used to log into a remote machine securely using your key pair. SSH traffic means encrypted commands and responses travelling between your computer and the EC2 instance over that secure connection.

### To enable direct access, I set up key pairs

Key pairs are a pair of digital keys used like a secure login system for your servers. One key stays on the server, and the other stays on your computer. When you try to connect, they match up to prove it’s really you, keeping your server safe from strangers.

A private key's file format means it is the type of file used to store the key, similar to how documents can be saved as PDF or DOCX. My private key's file format was .pem

## Launching a public server

I had to change my EC2 instance's networking settings by editing the network settings panel, selecting NextWork VPC and my public subnet from the drop-down (instead of the default VPC), and choosing the existing NextWork Public Security Group as the firewall before launching.

### ✍️ What are we doing in this step?

In this step, I will launch a private EC2 instance in my private subnet and create a security group that allows traffic from my public server because this sets up a secure environment where the private server is protected from the internet and can only communicate with trusted resources.

![Launching a public server](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_88727bef)

## Launching a private server

My private server has its own dedicated security group because it prevents random internet traffic from reaching it. By allowing access from the public server's security group, I ensure that only trusted internal resources can communicate with the private instance, keeping the network secure

My private server's security group's source is the NextWork Public Security Group, which means only resources in that group (like my public server) can reach it. Random internet traffic is blocked.

### ✍️ What are we doing in this step?

In this step, I will create my entire VPC setup using the "VPC and more" wizard instead of building each piece one by one because it saves time by creating all the resources, like subnets, route tables, and internet gateways, in a single go while showing me a visual map of how they connect.

![Launching a private server](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_4a9e8014)

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the VPC wizard to create the VPC, subnets, route tables, and internet gateway all at once. It saved time and showed me a visual map of how everything connects

A VPC resource map is a visual diagram that shows all the resources in your VPC and how they connect, like which subnets use which route tables and which ones reach the internet gateway. It makes understanding and troubleshooting your network setup much easier at a glance

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing VPC because AWS VPCs are isolated from each other by default, so there won't be any IP conflicts unless you explicitly connect them using VPC peering.

![Speeding up VPC creation](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_1cbb1b88)

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: 0 or 2. This was because AWS requires redundancy across Availability Zones for high availability. Having at least one public subnet in each zone ensures resources stay accessible if one goes down

The setup page also offered to create NAT gateways, which are services that let instances in private subnets access the internet for updates while blocking incoming traffic. This keeps your private servers safe from external threats without needing public IP addresses.

![Speeding up VPC creation](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/8f49d756-9e51-58c0-856a-e71e54f064ab_8ee57662)
