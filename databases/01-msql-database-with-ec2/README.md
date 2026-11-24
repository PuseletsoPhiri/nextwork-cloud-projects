<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Aurora Database with EC2

**Project Link:** [View Project](https://nextwork.ai/projects/cee72c3a-f285-55a6-8217-3cee4023a3bf)

---

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create an Amazon Aurora database and connect it to an EC2 instance. I'm doing this project to learn how to link a database service to a web server in AWS.

### ✍️ What are we doing in this step?

In this step, I will log in to the AWS Management Console using an IAM user because using an IAM user instead of the root user enhances security by keeping the master account key safe from everyday tasks and potential breaches.

### What is Amazon Aurora?

Amazon Aurora is a fast and reliable database service in AWS. It is useful because it keeps data safe and available using clusters, though I chose standard MySQL instead since Aurora is not available on my free tier plan.

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to store data for my web app. Since it was not available on my free tier, I used standard MySQL instead

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that Aurora would be unavailable on my free tier plan. I had to use standard MySQL instead.

### This project took me...

This project took me about one hour to complete

### ❤️ Thanks for doing this project!

I chose to do this project today because I want to learn how to connect a database to a web server in AWS. Something that would make learning with NextWork even better is showing more free tier alternatives when a service like Aurora is not available on a free plan.

## In the first part of my project...

### Creating an Aurora Cluster

A relational database is a type of database that organises data into tables with rows and columns, like a spreadsheet. The rows relate to the columns, which lets you query the data using SQL (Structured Query Language).

Aurora is a good choice when you need high performance and uptime for large scale projects. Since Aurora is not available on my free tier plan, I chose standard MySQL instead.

![In the first part of my project...](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/cee72c3a-f285-55a6-8217-3cee4023a3bf_44443546)

## Halfway through I stopped!

I stopped creating my MySQL database because I need to connect it to an EC2 instance. Since the instance doesn't exist yet, I have to create it first before finishing the database setup.

### ✍️ What are we doing in this step?

In this step, I will launch an EC2 instance because I need a virtual server to host my web app in the next project.

### Features of my EC2 instance

I created a new key pair for my EC2 instance because it acts as the login credentials to access the server. I need it to connect via SSH and manage the instance.

When I created my EC2 instance, I took particular note of the public IPv4 DNS and the key pair name. The DNS is like the address of my house, and the key pair is the key that lets me in.

### ✍️ What are we doing in this step?

In this step, I will finish creating my MySQL database and connect it to my EC2 instance because I need the database and web server to work together.

![Halfway through I stopped!](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/cee72c3a-f285-55a6-8217-3cee4023a3bf_91b9fd1g)

## Then I could finish setting up my database

![Then I could finish setting up my database](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/cee72c3a-f285-55a6-8217-3cee4023a3bf_1fddb0b5)

Aurora Database uses clusters because they keep your data safe and always available. If the main database fails, a backup copy takes over automatically.
