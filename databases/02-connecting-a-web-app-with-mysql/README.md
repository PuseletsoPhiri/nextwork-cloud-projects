<picture><source media="(prefers-color-scheme: dark)" srcset="https://nextwork.ai/static/nextwork-logo-paper.svg" /><img src="https://nextwork.ai/static/nextwork-logo-leather.svg" alt="NextWork" width="300" /></picture>

# Connect a Web App with Aurora

**Project Link:** [View Project](https://nextwork.ai/projects/921d7b78-ffa4-5e41-a5b5-aed76c78efad)

---

![](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1709b26b)

## Introducing Today's Project!

### ✍️ What are we here to do today?

In this project, I will demonstrate how to create a MySQL database and connect it to an EC2 instance. I'm doing this project to learn how to link a database to a web server since Aurora is unavailable on my free tier.

### ✍️ What are we doing in this step?

In this step, I will log in with an IAM user because it is safer than using the root account.

### ✍️ What are we doing in this step?

In this step, I will launch an EC2 instance because it acts as the virtual computer that hosts my web app.

### ✍️ What are we doing in this step?

In this step, I will create a MySQL database from scratch because it stores data for my web app since Aurora is unavailable on my free tier.

### ✍️ What are you doing in this step?

In this step, I will connect to my EC2 instance with SSH and install a basic web app because the server needs software to run the site that talks to my MySQL database.

### What is Amazon Aurora?

Amazon Aurora is a fast and reliable database service in AWS. It is useful because it keeps data safe and available using clusters, though I chose standard MySQL instead since Aurora is not available on my free tier plan.

### How I used Amazon Aurora in this project

In today's project, I used Amazon Aurora to store employee data for my web app. Since it was not available on my free tier, I used standard MySQL instead.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that Aurora would be unavailable on my free tier plan. I had to use standard MySQL instead.

### This project took me...

This project took me about one hour to complete.

### ❤️ Thanks for doing this project!

I chose to do this project today because I want to learn how to connect a database to a web server in AWS. Something that would make learning with NextWork even better is showing more free tier alternatives when a service like Aurora is not available on a free plan.

## Creating a Web App

![Creating a Web App](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_b7999168)

To connect to my EC2 instance, I used SSH with the key pair file I downloaded when I created it.

To help me create my web app, I first installed Node.js and the MySQL driver so my server could run the site and talk to my database.

### ✍️ What are we doing in this step?

In this step, I will create a folder and PHP script because it builds the web page that lets users see and use my MySQL database.

## Connecting my Web App to Aurora

I set up my EC2 instance's connection details to my database by creating a dbinfo.inc file. This file stores the server address, username, password, and database name so my app can connect to MySQL.

![Connecting my Web App to Aurora](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1709b25b)

## My Web App Upgrade

Next, I upgraded my web app by adding a PHP script. This lets users type in names and addresses to save them into my MySQL database.

### ✍️ What are we doing in this step?

In this step, I will test my web app in the browser and check the database with MySQL CLI because it proves data saves correctly

![My Web App Upgrade](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_2709b25b)

## Testing my Web App

To make sure my web app was working correctly, I entered data in the web form. Then I ran a MySQL query to check if it appeared in the database.

![Testing my Web App](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/921d7b78-ffa4-5e41-a5b5-aed76c78efad_1409z22b)
