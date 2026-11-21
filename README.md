# NextWork Cloud Projects

Hands-on AWS projects I'm completing through NextWork's **[Cloud Engineer Roadmap](https://nextwork.ai/portfolio/illusionmenon/learnlists/7bcf077e-33d8-5cca-b2b7-c69f43316fb0)**, a 45-project learning path covering the essential skills for a cloud engineer. Each project has its own folder with a README explaining what I built, what went wrong, and what I learned.

This sits alongside my other portfolios:
- [AWS Cloud Portfolio](https://github.com/PuseletsoPhiri/aws-cloud-portfolio): the week-by-week CSN AWS bootcamp tasks
- [NextWork AI Projects](https://github.com/PuseletsoPhiri/nextwork-ai-projects): beginner AI projects with v0, n8n, and CrewAI

## Progress

**10 of 45 projects complete.** Currently starting the database projects.

### Foundations: storage and security

| # | Project | Status | Details |
|---|---------|--------|---------|
| 2 | [Host a Website on Amazon S3](https://nextwork.ai/projects/70e2d059-31ab-5f67-8c58-f5edbd451140) | ✅ Done | [Project folder](hosting-a-website-on-s3) |
| 3 | [Cloud Security with AWS IAM](https://nextwork.ai/projects/51a5fd24-7458-58a6-8653-9b90119a0e4a) | ✅ Done | [Project folder](cloud-security-with-aws-iam) |

### Networking: the VPC series

| # | Project | Status | Details |
|---|---------|--------|---------|
| 4 | [Build a Virtual Private Cloud](https://nextwork.ai/projects/7f907ac7-2473-5c15-a8be-edb36581cdba) | ✅ Done | [Project folder](amazon-vpc/01-build-a-vpc) |
| 5 | [VPC Traffic Flow and Security](https://nextwork.ai/projects/fe5ed473-5874-57e1-a58f-d9b3d652330c) | ✅ Done | [Project folder](amazon-vpc/02-vpc-traffic-flow-and-security) |
| 6 | [Creating a Private Subnet](https://nextwork.ai/projects/4e96e29d-98b8-551e-ae93-da39c36e30fd) | ✅ Done | [Project folder](amazon-vpc/03-creating-a-private-subnet) |
| 7 | [Launching VPC Resources](https://nextwork.ai/projects/8f49d756-9e51-58c0-856a-e71e54f064ab) | ✅ Done | [Project folder](amazon-vpc/04-launching-vpc-resources) |
| 8 | [Testing VPC Connectivity](https://nextwork.ai/projects/da091986-ef01-5973-a070-b15e174f59d8) | ✅ Done | [Project folder](amazon-vpc/05-testing-vpc-connectivity) |
| 9 | [VPC Peering](https://nextwork.ai/projects/fd75209e-d2a1-5bdd-90e8-bdb9ee49de16) | ✅ Done | [Project folder](amazon-vpc/06-vpc-peering) |
| 10 | [VPC Monitoring with Flow Logs](https://nextwork.ai/projects/6954a600-a89e-56b0-886b-7054da118a3b) | ✅ Done | [Project folder](amazon-vpc/07-vpc-monitoring-flow-logs) |
| 11 | [Access S3 from a VPC](https://nextwork.ai/projects/36d7dc8f-3a9f-51ff-91ae-662077ea9920) | ✅ Done | [Project folder](amazon-vpc/08-access-s3-from-a-vpc) |

### Databases: currently working on

| # | Project | Status |
|---|---------|--------|
| 13 | [Aurora Database with EC2](https://nextwork.ai/projects/cee72c3a-f285-55a6-8217-3cee4023a3bf) | 🔄 In progress |
| 14 | [Connect a Web App with Aurora](https://nextwork.ai/projects/921d7b78-ffa4-5e41-a5b5-aed76c78efad) | ⬜ Not started |
| 15 | [Load Data into DynamoDB](https://nextwork.ai/projects/8bd82466-f5ee-569e-9125-2c4c6ce7a07f) | ⬜ Not started |
| 16 | [Query Data with DynamoDB](https://nextwork.ai/projects/0001cf4c-8256-52ae-b09c-6e99ed36462f) | ⬜ Not started |

## Skills practised so far

| Area | What I've used |
|------|----------------|
| AWS foundations | S3 static website hosting |
| Identity and access | IAM users, groups, and policies |
| Networking | VPCs, public and private subnets, VPC traffic flow and security, peering, Flow Logs, S3 access from a VPC |
| Troubleshooting | Testing connectivity and tracing traffic between VPC resources |

## Repository structure
```
nextwork-cloud-projects/
├── README.md
├── amazon-vpc/
│   ├── 01-build-a-vpc/
│   ├── 02-vpc-traffic-flow-and-security/
│   ├── 03-creating-a-private-subnet/
│   ├── 04-launching-vpc-resources/
│   ├── 05-testing-vpc-connectivity/
│   ├── 06-vpc-peering/
│   ├── 07-vpc-monitoring-flow-logs/
│   └── 08-access-s3-from-a-vpc/
├── cloud-security-with-aws-iam/
│   └── README.md
└── hosting-a-website-on-s3/
    └── README.md
```

## Cost control
After documenting each project, I delete the resources I created so the account avoids unexpected charges.

## Security note
No access keys, passwords, or account credentials are stored in this repository. Screenshots are cropped or blurred where they would show an account ID or other private details.

## About
I'm Puseletso Phiri, an IT graduate from South Africa building skills in cloud and AI.

- GitHub: [PuseletsoPhiri](https://github.com/PuseletsoPhiri)
- Email: khalabiphiri@protonmail.com
