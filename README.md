
# Cloud Security with AWS IAM


---

## Introducing Today's Project!

In this project, I will demonstrate my understanding of AWS IAM services and AWS EC2. I'm working on this project to learn more about cloud security and its applications in the real world.

### Tools and concepts

Services I used were Amazon EC2 and IAM systems. Key concepts I learnt include how to create an instance, create tags for an instance, how to create IAM policies, user groups, users, and account aliases.

### Project reflection

This project took me approximately one hour and fifteen minutes. The most challenging part was that I messed up the name on my JSON file and had to correct it. It was most rewarding to successfully stop the instance as a user.

---

## Tags

Tags are similar to names given to instances. They're helpful because mutliple instances can have the same or similar tags and it makes them easier to sort and manage your systems.

The tag I’ve used on my EC2 instances is called the ENV tag, short for environment. The value I’ve assigned for my instances is Prod, short for production, and Dev, short for development.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

IAM Policies are rules that determine who can use what resources in a system, like instances, databases, servers and more.

### The policy I set up

For this project, I’ve set up a policy using the JSON policy editor

I’ve created a policy that allows the user to view all EC2 instances. I've also created a policy that allows them full access to EC2 instances with the tag ENV and value Dev, and I've made sure they can't create or delete instances.

### When creating a JSON policy, you have to define its Effect, Action and Resource.

The Effect, Action, and Resource attributes of a JSON policy means the action, the resource, and the actions in that resource. Effect allowa access to the resource, action is what they can do in the resource, and resource is the name of the resource.

---

## My JSON Policy

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_1c864649)

---

## Account Alias

An account alias is another way of identifying yourself in AWS, it uses a name instead of an account ID number, making it more user friendly.

Creating an account alias took me less than a minute. Now, my new AWS console sign-in URL is https://nextwork-alias-alvin.signin.aws.amazon.com/console

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### Users

IAM users are users who have been given access to AWS resources.

### User Groups

IAM user groups are the collection of users who have access to a resource.

I attached the policy I created to this user group, which means that every user in the group is subject to my policies and their subsequent restrictions.

---

## Logging in as an IAM User

The first way is to download it as a CSV file, the second way is to email the user the instructions.

Once I logged in as my IAM user, I noticed that I could not see much of the information that you are usually provided with in regard to your AWS environment. This was because I configured my policies to only allow users to see specific resources.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

I tested my JSON IAM policy by first trying to stop the Prod EC2 instance, then by trying to stop the DEV EC2 instance.

### Stopping the production instance

When I tried to stop the production instance, I was met with an error message telling me I did not have permission to perform this action. This was because I made it so that the user could only access the Dev instance.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_0e7a9d6a)

---

## Testing IAM Policies

### Stopping the development instance

Next, when I tried to stop the development instance, I was successful in doing so. This was because I gave the user full access to the resource.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-iam_1811801c)

That marks the end of this project, if you've made it this far, thank you.
