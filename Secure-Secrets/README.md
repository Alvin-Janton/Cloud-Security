
# Secure Secrets with Secrets Manager



---

## Introducing Today's Project!

In this project, I will demonstrate how to use AWS SecretsManager to manage sensitive information from being exposed in one's code. I'm doing this project to learn more about cybersecurity and cloud security.

### Tools and concepts

Services I used were AWS SecretsManager, git, and GitHub. Key concepts I learnt include how to use SecretsManager to securely use sensitive variables, how to fork a repository using git, and how to resolve merge conflicts.

### Project reflection

This project took me approximately one and a half hours to complete. The most challenging part was trying to figure out how to resolve the git merge conflict. The most rewarding part was resolving the git merge conflict and pushing the code successfully.

I did this project today to learn more about cloud security. This project has helped me in learning how to secure sensitive data using SecretsManager.

---

## Hardcoding credentials

In this project, a sample web app is exposing its AWS keys on a public GitHub repo. It is unsafe to hardcode credentials because if you share the code publicly, anyone who sees the code could steal your credentials and log into your AWS environment.

I've set up the initial configuration by hardcoding the AWS access key, AWS secret key, and the region. These credentials are just examples because exposing my real AWS credentials would be a massive security risk.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

---

## Pushing Insecure Code to GitHub

Once I updated the web app code with credentials, I forked the repository because this was the fastest way to make a public repository with the necessary code. A fork is different from a clone; a cloned repository is a local repo that sits on your computer and isn't viewable by other people.

To connect my local repository to the forked repository, I used git init to initialize my local repo to the public one on GitHub, then I used git remote set url -origin to change the origin URL to the forked repo. Then I used git add and git commit to commit my changes and prepare to push the code. Finally, git push uploads my changes to the config.py file to the GitHub repo.

GitHub blocked my push because GitHub Secrets Scanner noticed that I was trying to push hardcoded AWS credentials into a public repository. This is a good security feature because it ensures that no one accidentally pushes compromising code.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is a service that securely maintains authentication keys for a variety of different services and applications. I'm using it to store my AWS credentials for the web app. Other common use cases include database encryption keys, API keys, and authentication tokens.

Another feature in Secrets Manager is secrets rotation. Secrets rotation is the process of changing the secrets after a specified amount of time has passed. It's useful in situations where you want to make an object as secure as possible. If my AWS credentials got compromised by a hacker, after the secrets are rotated, the hacker will no longer have access.

Secrets Manager provides sample code in various languages, like Java, Python, JavaScript, and C#. This is helpful because it makes it shows how to write the code to access the credentials.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the config.py file to retrieve the secret keys from SecretsManager. The get_secret() function will connect the code to SecretsManager by using a session client.

I also added code to config.py to extract the AWS credentials from SecretsManager. This is important because if the app.py file uses these credentials to function properly, without it the web app will fail.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is the process of interacting with your previous git commits. I used it to drop the previous commit from the commit history. This was necessary because the previous commit had a config.py file that still had hardcoded credentials.

A merge conflict occurred during rebasing because git was unsure of what to do with the previous config.py file and the current one. I resolved the merge conflict by removing the code from the previous commit with the hardcoded values.

Once the merge conflict was resolved, I verified that it worked by pushing the code to my GitHub repository and checked the config.py file to make sure there were no credential leaks.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
