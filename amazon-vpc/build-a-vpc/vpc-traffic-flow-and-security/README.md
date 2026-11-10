## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to control traffic flow and secure an Amazon VPC by creating a route table, a security group, and a network ACL. I'm doing this project to learn how data travels through a VPC (from user request to EC2 instance and back) and how each component plays its part: route tables act as the GPS for traffic, security groups guard individual resources, and Network ACLs guard entire subnets.

### ✍️ What are we doing in this step?

In this step, I will create a VPC, a public subnet, and an Internet Gateway because these are the foundational pieces needed to build an isolated network in AWS. The VPC is the network itself, the subnet is a section of that network, and the Internet Gateway allows that network to connect to the internet.

### ✍️ What are we doing in this step?

In this step, I will create a route table and add a route that directs internet-bound traffic (0.0.0.0/0) to the Internet Gateway because this setup allows resources in the public subnet to communicate with the internet.

### What is Amazon VPC?

Amazon VPC is a private, isolated section of the AWS Cloud where you can launch resources in a virtual network that you define. It is useful because it gives you full control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to build an isolated network and control how traffic flows in and out. I created a route table to send internet-bound traffic to the Internet Gateway, a security group to allow HTTP access to my resources, and a Network ACL to add subnet-level security.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that custom Network ACLs deny all traffic by default, forcing you to explicitly allow traffic rather than just allowing it and blocking specific threats.

### This project took me...

This project took me about 1 hour, including writing notes/documentation, creating the route table, security group, and Network ACL, plus the secret mission.

## Route tables

Route tables are like a GPS for your network. They contain a set of rules, called routes, that tell traffic where to go. For example, if a server wants to send data to the internet, the route table points it toward the Internet Gateway. If the data is staying inside your VPC, the route table keeps it on the local network.

Routes tables are needed to make a subnet public because they act like a map that tells traffic where to go. Without a route pointing to the Internet Gateway, data has no path to leave the VPC. Adding that route gives your subnet the "key" to the internet.

## Route destination and target

Routes are defined by their destination and target, which means the destination is the address the traffic wants to reach, and the target is the path it takes to get there. e.g., it is like planning a road trip. The destination is the city you want to visit and the target is the specific highway or exit you take to get there.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of NextWork IG

### ✍️ What are we doing in this step?

In this step, I will create a security group with an inbound rule allowing HTTP traffic (port 80) from anywhere because a security group acts like a security guard at the door of each resource, and without it, nothing can reach my website.

![Route destination and target](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_0a07b191)

## Security groups

Security groups are like a security guard at the entrance of your server. They check who is allowed to enter or leave based on specific rules like port numbers and IP addresses. They work at the instance level to protect individual resources.

### Inbound vs Outbound rules

Inbound rules are  like a bouncer at a club door. They decide who is allowed to enter your server from the outside world. I configured an inbound rule that allows HTTP traffic on port 80 from any IP address so anyone can visit my website

Outbound rules are like a bouncer at the back door. They decide who is allowed to leave your server and go out into the world. By default, my security group's outbound rule allows all outbound traffic to any destination.

### ✍️ What are we doing in this step?

In this step, I will create a Network ACL with inbound and outbound rules allowing all traffic and associate it with my Public 1 subnet because a Network ACL acts like a traffic cop at the edge of the subnet, adding a second security layer that checks every data packet before it reaches my resources.

![Security groups](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_92b0b0b4)

## Network ACLs

Network ACLs are like traffic cops at the edge of your subnet. They check every data packet before it enters or leaves, adding a second layer of security at the subnet level.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that a security group protects individual resources (like an EC2 instance) and is stateful, while a network ACL protects the entire subnet and is stateless, meaning return traffic must be explicitly allowed.

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will allow all traffic in and out.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all traffic

![Default vs Custom Network ACLs](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_4faeb056)

## Tracking VPC Resources

I created additional VPC resources: a VPC, an internet gateway, and a security group. Instead of my usual region, I used us-east-1 (N. Virginia). Teams would use multiple regions to reduce latency for users closer to them and keep apps running if one region has an outage.

EC2 Global View is a tool where you can find all your EC2 and VPC resources (like VPCs, subnets, security groups, and internet gateways) across every AWS region in one dashboard. I could even narrow down my search by resource type or region. Without EC2 Global View, you'd have to switch regions one at a time to hunt for each resource.

Now that I've learnt about EC2 Global View, I'd use it again to audit my infrastructure across all regions after a major deployment to ensure all resources are accounted for and properly tagged.

![Tracking VPC Resources](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/fe5ed473-5874-57e1-a58f-d9b3d652330c_b03ea6162)
