<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](https://nextwork.ai/projects/51a5fd24-7458-58a6-8653-9b90119a0e4a)

**Author:** khalabiphiri@protonmail.com  
**Email:** khalabiphiri@protonmail.com

---

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_1c864649)

## Introducing Today's Project!

### Project overview

In this project, I will demonstrate how to use AWS IAM to control access and permission settings in my AWS account. I'm doing this project to learn about cloud security from the foundation

### Tools and concepts

Services I used were Amazon EC2 and AWS IAM. Key concepts I learnt include IAM users, roles, groups, policies and account aliases

### Project reflection

This project took me approximately 10 minutes. The most challenging part was the policy simulator; it was different from the one shown in the example. It was most rewarding to be able to navigate the policy simulator and complete the task.

## Tags

### What I did in this step

In this step, I will launch two EC2 instances because there will be increased traffic to the NextWork website as more students want to learn during their holidays. These instances will boost the computing power of the NextWork website as more students board the NextWork platform. 

### Understanding tags

Tags are organisational tools that let us label our resources; they are helpful for grouping resources, cost allocation and applying policies for all resources with the same tag.

### My tag configuration

The tag I’ve used on my EC2 instances is called `env`, which stands for `environment`. The value I’ve assigned for my instances is production and development

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_2e0e5a5d)

## IAM Policies

### What I did in this step

In this step, I will use IAM policies to control the access level of the new NextWork intern because they should not have access to the production environment

### Understanding IAM policies

IAM policies are rules that define what actions are allowed or denied on resources. I am using policies today to control who has access to our environment/production instance

### The policy I set up

For this project, I’ve set up a policy using a JSON

### Policy effect

I’ve created a policy that allows the policyholder, i.e., the intern, to have permission to do anything they want to any instance tagged with 'development'. They can also see any information related to any instance, but they are denied access to creating and deleting tags for any instance

### Understanding Effect, Action, and Resource

The Effect, Action, and Resource attributes of a JSON policy mean whether or not the policy is allowing or denying action, which is the effect. What the policy holder can and cannot do (i.e., the action) and the specific AWS resources that the policy is related to (i.e., the resource)

## My JSON Policy

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_1c864649)

## Account Alias

### What I did in this step

In this step, I will set up an account alias, which is like a nickname for our AWS account login because it makes it simpler for your users to login in.

### Understanding account aliases

An account alias is basically a name that you can use instead of your account ID

### Setting up my account alias

Creating an account alias took me less than two minutes. Now, my new AWS console sign-in URL uses my alias instead of my account ID.

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_0eb4439b)

## IAM Users and User Groups

### What I did in this step

In this step, I will set the IAM users and IAM groups for NextWork interns because IAM users are like logins for people who want to access our AWS account, whereas IAM groups are like folders to manage users that have the same level of access.

### Understanding user groups

IAM user groups are folders of users for easier user management

### Attaching policies to user groups

I attached the policy I created to this user group, which means all the users in this group will have the same permissions

### Understanding IAM users

IAM users are individuals who access AWS

## Logging in as an IAM User

### Sharing sign-in details

The first way is to email instructions to the user and the second way is to download the CSV file with the login details inside

### Observations from the IAM user dashboard

Once I logged in as my IAM user, I noticed that our user has been denied access to panels on the main AWS dashboard. This was because I only set up permissions for our development EC2 instance so our intern wouldn't have access to see anything else

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_6f2ab446)

## Testing IAM Policies

### What I did in this step

In this step, I will login into AWS using the intern's IAM user to test the intern's access to our production and development instances because I want to make sure our intern doesn't have the ability to do anything that will affect our production environment

### Testing policy actions

I tested my JSON IAM policy by stopping two of the instances, of which one 'production environment' failed to stop, as the user didn't have permission. The user was able to stop the 'development environment' because they had the permission for the instance

### Stopping the production instance

When I tried to stop the production instance, a popup error appeared: 'Failed to stop instance'. This was because our user doesn't have the permission for this instance

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_0e7a9d6a)

### Stopping the development instance

Next, when I tried to stop the development instance, the instance state successfully stopped. This was because the user had the permission to stop instances

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_1811801c)

## IAM Policy Simulator

To extend my project, I'm going to test my policies and permission in a safer and more controlled way with a tool called IAM Policy Simulator. I'm doing this because having to stop instances and log into the AWS account as other users can be a bit disruptive

### Understanding the IAM Policy Simulator

The IAM Policy Simulator is a tool that lets us simulate actions and test permission settings by defining a specific user, role, group and the action we want to test for. It's useful for saving time when testing user permission settings. No more logging into another user's account to test permission settings

### How I used the simulator

I set up a simulation to check whether our dev user group has the permissions to StopInstances or DeleteTags. The results were denied for both, so I had to adjust the scope of the EC2 instances to ones that are tagged with development. Once I applied that tag the permission was allowed

![Image](https://nextwork.ai/exuberant_purple_zany_armadillo/uploads/51a5fd24-7458-58a6-8653-9b90119a0e4a_069d8a621)

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/51a5fd24-7458-58a6-8653-9b90119a0e4a)*
