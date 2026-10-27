<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Host a Website on Amazon S3

**Project Link:** [View Project](https://nextwork.ai/projects/70e2d059-31ab-5f67-8c58-f5edbd451140)

**Author:** khalabiphiri@protonmail.com  
**Email:** khalabiphiri@protonmail.com

---

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_5d4474f9)

## Introducing Today's Project!

### Project overview

In this project, I will demonstrate how to use s3 to host static websites... I'm doing this project to learn about AWS and cloud services and how they can be used to store objects in the cloud and even host websites

### Tools and concepts

Services I used were Amazon S3. Key concepts I learnt include bucket policies and uploading the static website file 'index.html', bucket endpoint URLs and ACLs and how they control access to our bucket objects

### Time, challenges, and wins

This project took me approximately 20 minutes, including answering questions about the project. The most challenging part was resolving the 403 Forbidden Error. It was most rewarding to see my website load live and be public to the world

## How I Set Up an S3 Bucket

### What I did in this step

In this step, I will open S3 and create storage for my website files

### How long it took to create the bucket

Creating an S3 bucket took me... less than 7 minutes. I needed to learn a few concepts like blocked access and ACLs, but once that learning is done, I can create buckets in a shorter time in the future

### Region selection

The region I picked for my S3 bucket was Cape Town... because it is the closest region to me. It is best practice to pick a region closest to you to reduce latency (time to retrieve data) and costs

### Understanding bucket name uniqueness

S3 bucket names are globally unique! This means... no two Amazon buckets in the entire world can have the same name; they have to be unique regardless of a region or AWS account ID

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_ba6d42ad)

## Upload Website Files to S3

### What I did in this step

In this step, I will upload files in my S3 bucket because no files mean no website.

### Files I uploaded

I uploaded two files to my S3 bucket – they were index.html, which holds the structure of my website and a folder which holds the images and assets of the website

### How the files work together

Both files are necessary for this project, as the index.html determines the structure, but the structure alone doesn't illustrate the content of the website, i.e., if the index.html says 'insert an image here', it might not have the actual image to display; you would need to supply the image separately. That's why i have multiple files uploaded separately

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_a265af88)

## Static Website Hosting on S3

### What I did in this step

In this step, I will make my website available to the world! This is called static website hosting, and it is important because my website files will stay as "just files" and not turn into a website if I don't do this step

### Understanding website hosting

Website hosting means uploading my website files on a web server, which is a special computer that will turn these files into a web page/s that people can visit

### How I enabled website hosting

To enable website hosting with my S3 bucket, I went to the properties tab and enabled static website hosting, and I labelled the index document 'index.html'.

### Access Control Lists (ACLs)

An ACL is... a way to configure permissions settings inside a bucket. I enabled ACL so that I can control access to my website files later. I've kept it enabled to learn how ACLs work and compare it with bucket policies later

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_c22c54c0)

## Bucket Endpoints

### Understanding bucket endpoint URLs

Once a static website is enabled, S3 produces a bucket endpoint URL, which is a URL that gives people access to my S3 bucket as a website 

### What I saw when I tested the endpoint

When I first visited the bucket endpoint URL, I saw a 403 Forbidden Error. The reason for this error was that objects are public by default, even though I switched off 'block all public access'. The website files themselves are still completely private, but I need to manage their access settings separately

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_22ce4daf)

## Success!

### What I did in this step

In this step, I will go into the files I've uploaded in my bucket and make them public too because this will enable me and the public to actually view the contents of my website and once that is done my website will be officially live

### How I resolved the 403 error

To resolve this 403 Forbidden error, I went to the buckets objects and made them public using ACLs

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_5d4474f9)

## Bucket Policies

### What I did in this extension

In this project extension I'm about to use bucket policies to control access to my bucket files. I'm doing this so that I can stop people from deleting the objects inside the files

### Understanding bucket policies

An alternative to ACLs is bucket policies, which are rules that determine who is allowed access (or denied access) to do something. The benefit of using bucket policies is that you can have greater control over actions that people are allowed/not allowed to do, while ACLs are useful for controlling public access to individual objects inside the bucket

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/70e2d059-31ab-5f67-8c58-f5edbd451140_sm2sm2sm)

### What my bucket policy does

My bucket policy prevents anyone from deleting the file. I tested this by trying to delete the 'index.html' file and saw a 'failed to delete objects' error

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/70e2d059-31ab-5f67-8c58-f5edbd451140)*
