<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Testing VPC Connectivity

**Project Link:** [View Project](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate VPC connectivity by connecting to my public server via EC2 Instance Connect, testing communication between my public and private servers using \`ping\` and verifying internet access with \`curl\`. I'm doing this project to learn how to troubleshoot security groups, network ACLs and routing to ensure data flows correctly within an AWS VPC.

### ✍️ What are we doing in this step?

In this step, I will set up the core VPC infrastructure, including subnets, gateway, and security configurations, because this creates the foundation needed to launch and connect EC2 instances securely

### ✍️ What are we doing in this step?

In this step, I will connect to my public server using EC2 Instance Connect and troubleshoot a connection issue because SSH access is blocked by the security group until I add an inbound rule.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you launch resources in a virtual network you define. It is useful because it gives you full control over your network environment, like choosing IP addresses and setting security rules while keeping your data secure and separate from other AWS customers.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create an isolated network where I securely launched and connected EC2 instances across public and private subnets while testing how data flows through security groups and network ACLs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how much of the connectivity troubleshooting comes down to checking security groups and network ACLs. Like locking both the gate and the front door, you have to open both for traffic to get through

### This project took me...

This project took me 1 hour, including documentation.

## Connecting to an EC2 Instance

Connectivity means how well different parts of your network can talk to each other and to the outside internet. It's what lets data flow smoothly, like how your phone needs a good signal to send messages. Without it, nothing works.

My first connectivity test was whether I could connect to my public server using EC2 Instance Connect

![Connecting to an EC2 Instance](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/da091986-ef01-5973-a070-b15e174f59d8_88727bef)

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a direct SSH access tool that manages keys for you. It is like using a hotel key card instead of carrying a heavy key ring. It generates a temporary key automatically so you can connect quickly without the hassle of manual setup

My first attempt at getting direct access to my public server resulted in an error because the security group was blocking SSH traffic. I needed to add an inbound rule to allow SSH connections from any IPv4 address so EC2 Instance Connect could reach the server

I fixed this error by editing the public server's security group to add an inbound SSH rule with the source set to Anywhere-IPv4, letting EC2 Instance Connect reach the server

### ✍️ What are we doing in this step?

In this step, I will make my public server talk to my private server using \`ping\` and troubleshoot a connection issue because the private subnet's network ACLs are blocking ICMP traffic by default.

![EC2 Instance Connect](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/da091986-ef01-5973-a070-b15e174f59d8_1cbb1b88)

## Connectivity Between Servers

Ping is a network tool that sends a tiny "are you there?" message to another device and checks if it gets a reply. I used ping to test the connectivity between my public server and private server, confirming they could talk across subnets once IMCP traffic was allowed.

The ping command I ran was ping 10.0.1.127, using my private server's private IPv4 address to check if it would reply from the public server.

The first ping returned one line with no replies. This meant the private server was not responding, likely because ICMP traffic was blocked by network ACLs or security groups.

![Connectivity Between Servers](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/da091986-ef01-5973-a070-b15e174f59d8_defghijk)

## Troubleshooting Connectivity

I troubleshooted this by allowing inbound and outbound ICMP traffic in the private NACL from 10.0.0.0/24, then adding an all-ICMP rule to the private security group as a source. Like opening the neighbourhood gate and the front door so the ping could get through.

### ✍️ What are we doing in this step?

In this step, I will test internet connectivity from my public server using \`curl\` because it confirms the VPC routing and security settings allow outbound traffic to the web.

![Troubleshooting Connectivity](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/da091986-ef01-5973-a070-b15e174f59d8_4a9e8014)

## Connectivity to the Internet

Curl is a command-line tool that transfers data to or from a server. It is like ordering takeout: you send a request (the order), and the server hands back the food (the data, like the webpage's HTML). I used it to prove my public server could reach the internet.

I used curl to test the connectivity between the public server and the internet. It confirmed that my server could fetch actual web content like HTML from external sites.

### Ping vs Curl

Ping and curl are different because ping just checks if the connection exists (like ringing a doorbell to see if someone's home), while curl actually fetches data from the server (like ordering food and getting it delivered).

## Connectivity to the Internet

I ran the curl command \`curl example.com\`, which returned the raw HTML content of the website, confirming my public server could successfully reach and fetch data from the internet

![Connectivity to the Internet](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/da091986-ef01-5973-a070-b15e174f59d8_8ee57662)
