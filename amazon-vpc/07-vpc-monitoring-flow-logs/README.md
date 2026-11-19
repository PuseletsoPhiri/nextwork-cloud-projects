<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](https://nextwork.ai/projects/6954a600-a89e-56b0-886b-7054da118a3b)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to monitor an AWS network by setting up VPC Flow Logs and analysing the captured traffic with CloudWatch. I'm doing this project to learn how to track inbound and outbound traffic between two peered VPCs, use IAM roles to grant Flow Logs permission to write to CloudWatch, troubleshoot connectivity issues with ping tests, and query log data in Logs Insights to see which IP addresses transfer the most data.

### What is Amazon VPC?

Amazon VPC is a virtual network isolated in the AWS cloud. It is useful because you get full control over your own network settings, like IP ranges and security rules, to keep your resources safe and organized.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create two isolated networks and connect them securely. I built a virtual highway between them using a peering connection so instances could talk directly. I also set up flow logs to act like a security camera tracking every packet moving through the network.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how much time troubleshooting took compared to setup. The ping tests failed at first because of a missing route table entry, not a security group issue. Fixing that one line made everything work instantly.

### This project took me...

This project took me approximately 1 hour including documentation

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will create two VPCs (NextWork-1 with CIDR 10.1.0.0/16 and NextWork-2 with 10.2.0.0/16), each with one public subnet, no private subnets, no NAT gateway, and no VPC endpoints, because I need two separate networks to generate and monitor traffic between them later in the project.

### Step 2 - Launch EC2 instances

In this step, I will launch one EC2 instance in each VPC with a security group allowing all ICMP traffic, because I need two live servers to ping each other so I have real network traffic for the flow logs to capture.

### Step 3 - Set up Logs

In this step, I will create a CloudWatch log group called NextWorkVPCFlowLogsGroup and start a VPC Flow Log on VPC 1 with the filter set to All and a 1-minute aggregation interval, because I need a place to store records of every packet entering or leaving my VPC so I can review that traffic later.

### Step 4 - Set IAM permissions for Logs

In this step, I will create an IAM policy and role that grants VPC Flow Logs permission to write logs to CloudWatch, because Flow Logs do not have these permissions by default and need a role to deliver traffic records to my log group.

## Multi-VPC Architecture

I started my project by launching two VPCs (NextWork-1 and NextWork-2) and created two subnets, one public subnet in each VPC.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because if the IP ranges overlap, the addresses clash and routing breaks, so traffic can't find its way between the two networks.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow all inbound ICMP traffic from 0.0.0.0/0. This is because the ping tests later in the project need ICMP packets to reach the instances from any source, not just the peered VPC.

![Multi-VPC Architecture](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_e7fa8775)

## Logs

Logs are like a diary for your systems. They record everything that happens, from users logging in to errors popping up, so you can troubleshoot problems and see who is doing what.

Log groups are like a big folder in CloudWatch that keeps related logs together. For example, all flow logs from your VPC go into one log group so you can find and search them in one place.

![Logs](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_e8398869)

### ✍️ What is a flow log?

Flow logs are like a diary for your VPC. They record every packet of data that enters or leaves your network interfaces so you can see exactly what traffic is moving through your network.

## IAM Policy and Roles

I created an IAM policy to give VPC Flow Logs the specific permission to create log streams and send traffic data to CloudWatch. Without this policy, the Flow Logs feature cannot write its records anywhere.

I also created an IAM role because I need to bundle the policy into a container that I can assign directly to the VPC Flow Logs service. The role acts as the identity that CloudWatch uses to write logs on my behalf.

A custom trust policy is like a VIP list. It specifies exactly which AWS service can use the role. This keeps your setup secure by preventing other services from accidentally using your permissions.

![IAM Policy and Roles](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_4334d777)

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will use EC2 Instance Connect to open Instance 1 and ping Instance 2's private IP address, because a successful reply proves the two VPCs can talk directly, and any failed replies give me real traffic for the flow logs to capture.

### Step 6 - Set up a peering connection

In this step, I will create a VPC peering connection and add routes in both VPCs so traffic flows directly between them, because without these routes the VPCs have no private path to each other, and instances cannot communicate using private IP addresses.

### Step 7 - Analyze flow logs

In this step, I will review the flow logs and use CloudWatch Logs Insights to query the data, because I need to analyse the network traffic and see which IP addresses transferred the most data.

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means the connection is broken. Instance 1 cannot reach Instance 2's private address, so there is no direct route between the two VPCs yet.

![Connectivity troubleshooting](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means Instance 2 is set up to answer pings and traffic can reach it over the public internet. So the instances work fine; they just lack a direct private route between the VPCs.

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because there was no route pointing to a VPC peering connection. The only path out was 0.0.0.0/0 through the internet gateway, so traffic to the private IP had nowhere direct to go.

### To solve this, I set up a peering connection between my VPCs

I updated both VPCs' route tables to add a route pointing each VPC's CIDR block at the peering connection. Without these routes, traffic had no direct private path between the VPCs and only knew how to exit through the internet gateway.

![Connectivity troubleshooting](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_7316a13d)

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means the peering connection is working, and the two VPCs can now communicate directly over their private networks.

![Connectivity troubleshooting](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_4ec7821f)

## Analyzing flow logs

Flow logs tell us about every network packet crossing your VPC. Each record shows the source and destination IP addresses, ports, protocol, bytes and packets transferred, whether the traffic was accepted or rejected, and the action taken by your security settings. For example, a log line might say 344 bytes went from 18.237.140.165 to 10.1.5.112 over TCP port 22 in 4 packets, with an ACCEPT at the end. That means SSH access succeeded. A line ending in REJECT is blocked traffic you should investigate.

For example, the flow log I've captured tells us traffic was rejected. The second line shows a REJECT OK status, meaning ICMP ping traffic from 45.156.128.155 to 10.2.4.218 was blocked by security groups. The third line shows an ACCEPT OK status, meaning traffic from 69.2.216.149 to 10.2.4.218 was allowed through on port 132.

![Analyzing flow logs](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_d116818e)

## Logs Insights

Logs Insights is a CloudWatch feature that analyses your logs. You use queries to filter, process and combine log data to troubleshoot problems or understand network traffic. For example, you can run a query to find the top 10 IP addresses transferring the most data in your VPC.

I ran the query "Top 10 byte transfers by source and destination IP addresses". This query analyses your flow logs to find the ten biggest data transfers between IP pairs, showing which resources move the most data across your network.

![Logs Insights](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/6954a600-a89e-56b0-886b-7054da118a3b_3e1e79a1)
