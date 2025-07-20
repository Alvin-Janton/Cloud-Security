
# Threat Detection with GuardDuty


---

## Introducing Today's Project!

### Tools and concepts

The services I used were CloudFormation, CloudShell, and GuardDuty. Key concepts I learnt include how to launch a web application using CloudFormation, how to do penetration testing for vulnerabilities, and how to configure GuardDuty to check for malware uploaded to an S3 bucket.

### Project reflection

This project took me approximately two hours to complete. The most challenging part was figuring out how to get the EICAR test file past my antivirus. It was most rewarding to see GuardDuty successfully detect the malicious file.

I did this project today to learn more about cloud security. This project is helping me in my goal to become a cloud security engineer.

---

## Project Setup

To set up for this project, I deployed a CloudFormation template that launches a web app that is purposely vulnerable. The three main components are the web app infrastructure, the S3 bucket, and GuardDuty.

The web app deployed is called OWSAP Juice Shop. To practice my GuardDuty skills, I will attack the web application to generate alerts from GuardDuty. Then, I will use these alerts to fix the vulnerabilities within the application.

GuardDuty is a threat detection service. In this project, it will pick up on and report indicators of attack and alert me.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_n1o2p3q4)

---

## SQL Injection

The first attack I performed on the web app was SQL injection, which means I inserted a malicious SQL code string into the SQL database to change how to database works. SQL injection is a security risk because it can allow attackers to steal information from a database or even delete the database, depending on the attack.

My SQL injection attack involved entering the string ' or 1=1;-- into the email text box. This means that I can skip the authentication section for this login.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_h1i2j3k4)

---

## Command Injection

Next, I used command injection, which is when you enter a script into a text field and the program runs that script when it isn't supposed to. The Juice Shop web app is vulnerable to this because it does not sanitize user input in the text fields.

To run command injection, I inserted a JS script into the username text field and clicked Set username. The script will tell the computer to go to the EC2 instance metadata and retrieve the AWS credentials, then it will make those credentials public for anyone to find and view.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_t3u4v5w6)

---

## Attack Verification

To verify the attack's success, I went to this URL "https://d1af7hm1ji58nx.cloudfront.net/assets/public/credentials.json". This URL page shows me the credentials for the AWS environment that I stole using the script.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_x7y8z9a0)

---

## Using CloudShell for Advanced Attacks

The attack continues in CloudShell because I want to simulate what an actual attacker would do in this circumstance, since I have ownership of the AWS environment.

In CloudShell, I used wget to download the credentials.json file. Next, I ran a command using cat and jq to output the contents of the file into the terminal.

I then set up a profile, called "stolen" to access the AWS environment. I had to create a new profile because AWS automatically assigns your profile to the CLI profile. This means GuardDuty won't send any alerts because it thinks it's me doing the actions.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_j9k0l1m2)

---

## GuardDuty's Findings

After performing the attack, GuardDuty reported a finding within a few minutes of the attack. Findings are reports of suspicious activity that takes place in your AWS environment.

GuardDuty's finding was called "UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS". This means that someone was able to get access to our AWS environment and steal data.

GuardDuty's detailed finding reported that the attacker logged in using our account credentials, retrieved information from our S3 bucket using the GetObject API.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_v1w2x3y4)

---

## Extra: Malware Protection

For my project extension, I enabled Malware Protection for S3, which will allow GuardDuty to scan and check for malicious files and stop them before they can harm the product. Malware is code or scripts whose purpose is to cause harm to the computer or service it's sent to.

To test Malware Protection, I uploaded an EICAR test malware file to my S3 bucket. The uploaded file won't actually cause damage because it has no malware inside of it; it just tricks software into thinking it's malware.

Once I uploaded the file, GuardDuty instantly triggered that it had scanned a malicious file uploaded to my S3 bucket object. This verified that GuardDuty is capable of detecting malware and sending out alerts within minutes.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-guardduty_sm42x3y4)

---
