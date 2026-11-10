<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# BUILD A VPC

## Introducing Today's Project!

In this project, I will demonstrate how to build the networking backbone of AWS by creating a Virtual Private Cloud (VPC), setting up public subnets, and attaching an internet gateway to enable secure communication between resources. I'm doing this project to learn about traffic rules and security measures to control how resources, like EC2 instances and databases, connect and work together.

## Virtual Private Clouds (VPCs)

### What I did in this step

In this step, I will create a VPC because without VPCs, every AWS resource would exist in one giant, open space in the cloud. VPCs are the reason why resources can be made private to me, and I get control over resources in a VPC to organise how they communicate and integrate with each other without the public internet.

### How VPCs work

VPCs are a private, isolated network where you launch AWS resources. e.g., like renting your own office building with private rooms and hallways.

### Why there is a default VPC in AWS accounts

There was already a default VPC in my account ever since my AWS account was created. This is because AWS creates one automatically when you sign up, so you can start using services like EC2 immediately without having to set up networking first.

![Virtual Private Clouds (VPCs)](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_2facf927)

### Defining IPv4 CIDR blocks

To set up my VPC, I had to define an IPv4 CIDR block, which is  simply the address range for my private network. e.g., it is like assigning street numbers to houses in a new neighbourhood. If I choose 10.0.0.0/16, I am reserving the entire range from 10.0.0.0 to 10.0.255.255 for my VPC. This ensures every resource I launch, like a server or database, gets a unique "street address" so they can find each other without any confusion or overlap.

## Subnets

### What I did in this step

In this step, I will add a subnet inside my VPC because my VPC is currently just a big empty space. I need to divide it into smaller neighbourhoods so I can organise my resources. For example, I can put public-facing web servers in one subnet and keep sensitive databases in a separate, private subnet. This helps me control who can access what and keeps my infrastructure secure.

### Creating and configuring subnets

Subnets are segments of your VPC network (public or private). There are already subnets existing in my account, one for every availability zone

### Public vs private subnets

The difference between public and private subnets is whether they can talk to the outside world. Public subnet = reception area (open to visitors). Private subnet = back office (staff only) For a subnet to be considered public, it has to be connected to an internet gateway so traffic can flow in and out of the internet. Naming it "Public 1" doesn't do that by itself. I also need a route table pointing internet-bound traffic to that gateway. Until both are in place, the subnet stays effectively private even if instances inside it have public IP addresses.

![Subnets](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_157c4219)

### Auto-assigning public IPv4 addresses

Once I created my subnet, I enabled auto-assign public IPv4 addresses. This setting makes sure that any EC2 instance launched in that subnet automatically gets a public IP address so that it can communicate with the internet without me having to create and assign one manually every time.

## Internet gateways

### What I did in this step

In this step, I will connect my VPC to the internet using an internet gateway because my resources need to communicate beyond my private space.

### Setting up internet gateways

Internet gateways are like the main front desk and security gate of your private office building. They provide the only official entry and exit point for traffic between your private network (VPC) and the outside internet. Without this gateway, my resources are stuck inside the building with no way to receive visitors or send mail out. Attaching it ensures my public instances can be accessed by users on the web and can download updates or connect to external services.

Attaching an internet gateway to a VPC means resources in your VPC can now access the internet. If I missed this step, my VPC would be completely cut off from the outside world.

![Internet gateways](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_4ae90410)

## Using the AWS CLI

### What I'm doing in this extension

In this project extension, I will use AWS CloudShell and the AWS CLI to create a VPC, subnet, and internet gateway using commands instead of clicking through the console.

I am doing this because engineers often prefer the command line for speed and automation. It lets me script tasks and manage resources more efficiently than manual clicks, which is a vital skill for real-world cloud work.

### Exploring CloudShell and CLI

VPC resources could also be created with CloudShell, which is a built-in browser terminal in AWS. It is like having a computer inside your account so you do not need to install extra software. CLI is the Command Line Interface. It is a tool that lets you control AWS using text commands instead of clicking buttons. It is faster and lets you automate tasks with scripts.

### Debugging my setup

To set up a VPC or a subnet, you can use the command aws ec2 create-subnet. Make sure to avoid errors by including the --cidr-block parameter. The CLI needs this specific range of IP addresses to know which numbers to assign inside the subnet. Without it, AWS doesn't have enough information to build the network section, so it throws a "MissingParameters" error.

![Using the AWS CLI](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/7f907ac7-2473-5c15-a8be-edb36581cdba_9b2465411)

### Comparing CloudShell vs AWS Console

Compared to using the AWS Console, an advantage of using commands is speed and automation. An advantage of using the console is that it is visual and beginner-friendly. You can see exactly where everything is located, which makes learning easier and reduces the chance of typing mistakes. Overall, I preferred the console for learning because it helped me understand the structure better, but I would use CloudShell for daily work once I am comfortable with the commands.
