<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# VPC Peering

**Project Link:** [View Project](https://nextwork.ai/projects/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16)

---

![](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_88727bef)

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create a VPC peering connection to link two separate VPCs together. I'm doing this project to learn how to route traffic between VPCs using private IP addresses without going through the public internet.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you launch resources in a virtual network you define. It is useful because it gives you full control over your network environment, like choosing IP addresses and setting security rules, while keeping your data secure and separate from other AWS customers.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create two separate virtual networks and connect them directly. This allowed secure communication between servers without going over the public internet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many small settings could break connectivity. Just one missing route or one blocked security group rule stopped the ping from working, which showed me that peering is only half the job and routing plus firewall rules are what actually let traffic flow.

### This project took me...

This project took me 1 hour including documentation

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two VPCs (NextWork-1 with CIDR 10.1.0.0/16 and NextWork-2 with CIDR 10.2.0.0/16) using the "VPC and more" wizard, because unique CIDR blocks prevent IP overlap and give me a working environment to peer later.

### Step 2 - Create a Peering Connection

In this step, I will create a peering connection between NextWork-1 and NextWork-2, because this link lets the two VPCs send traffic to each other using private IP addresses instead of going over the public internet.

### Step 3 - Update Route Tables

In this step, I will update the route tables in both VPCs to direct traffic to the peering connection, because without these routes the VPCs do not know how to send data to each other even if the connection exists.

### Step 4 - Launch EC2 Instances

In this step, I will launch one EC2 instance in each VPC (Instance - NextWork VPC 1 and Instance - NextWork VPC 2), because these instances act as the two computers on either side of my peering bridge so I can test that traffic actually flows between them.

## Multi-VPC Architecture

I started my project by launching two VPCs with the "VPC and more" wizard: NextWork-1 (10.1.0.0/16) and NextWork-2 (10.2.0.0/16). I created 2 subnets total, one public subnet in each VPC, with no private subnets, no NAT gateways, and no VPC endpoints.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because if they shared the same IP ranges, the network would not know which VPC to send traffic to, causing a conflict. It is like giving two houses on the same street the exact same house number.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances, as we are using EC2 Instance Connect, which manages the keys for us. This lets us skip the manual key setup and focus on testing the VPC peering connectivity.

![Multi-VPC Architecture](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_11111111)

## VPC Peering

A VPC peering connection is a direct link between two VPCs that lets them talk to each other using private IP addresses. It's like building a private bridge between two houses so you can visit without walking down the public road.

VPCs would use peering connections to share resources and send data between each other privately, without exposing traffic to the public internet. It's like a private tunnel between two office buildings so staff can walk over directly instead of going out onto the busy street.

The difference between a requester and an acceptor in a peering connection is that the requester is the VPC that starts the connection (sends the invite), while the acceptor is the VPC that receives it and must approve before the link works. It's like one person sending a friend request, and the other person has to hit "accept" before you're connected.

![VPC Peering](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_1cbb1b88)

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because the route table is what tells traffic where to go next. Without a route pointing at the peering connection, packets bound for the other VPC have nowhere to go and get dropped. It's like building a bridge between two towns but never putting up road signs telling drivers to take it.

My VPC's new routes have a destination of the other VPC's CIDR block. The routes' target was the VPC peering connection.

![Updating route tables](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_4a9e8014)

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will connect to Instance 1 using EC2 Instance Connect and fix the error it throws, because I need a shell on one side of the peering bridge before I can test traffic reaching VPC 2.

### Step 6 - Connect to EC2 Instance 1

In this step, I will fix the security group settings to allow SSH traffic and successfully connect to Instance 1, because the default security group blocks external access, and I need a working connection to test the VPC peering.

### Step 7 - Test VPC Peering

In this step, I will ping Instance 2 from Instance 1 and fix the ICMP blocking in the security group, because the default security group blocks ping traffic, and I need to confirm that data can flow across the peering bridge.

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to open a browser-based shell on Instance 1 without managing my own keys. It's like borrowing the library computer instead of bringing your own laptop, so I could run ping tests against VPC 2 right away.

I was stopped from using EC2 Instance Connect, as my instance had no public IPv4 address. I had set Auto-assign public IP to Disable, and EC2 Instance Connect needs a public IP plus a public subnet to reach the server over the internet.

![Troubleshooting Instance Connect](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7685490c)

## Elastic IP addresses

Elastic IP addresses are static public IPv4 addresses that stay with your account until you release them. They act like a permanent phone number for your server, so if the instance restarts or needs a new public IP, you can just swap the number over without changing any settings.

Associating an Elastic IP address resolved the error because it gave my instance the public IPv4 address it was missing. With that static public IP attached, EC2 Instance Connect could finally reach the server over the internet and open the browser shell.

![Elastic IP addresses](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_45663498)

## Troubleshooting ping issues

To test VPC peering, I ran the command \`ping 10.2.12.27\`. This sent small test messages to see if Instance 2 was reachable directly through the private peering connection.

A successful ping test would validate my VPC peering connection because it proves data successfully travelled across the private bridge between the two VPCs. It confirms that routing and security settings are working correctly, allowing direct private communication without the public internet.

I had to update my second EC2 instance's security group because the default settings blocked ping traffic. I added a new rule that allowed all ICMP traffic from VPC 1's IP range.

![Troubleshooting ping issues](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16_7a29d352)
