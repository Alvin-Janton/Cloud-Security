
# Encrypt Data with AWS KMS


---



## Introducing Today's Project!

In this project, I will demonstrate how to use AWS KMS to encrypt a database. The goal is to show how encryption can be used to enforce the confidentiality of data and prevent data breaches.

### Tools and concepts

Services I used include AWS KMS, DynamoDB, and AWS IAM. Key concepts I learnt include encryption, how to create a DynamoDB table, and how to grant access to KMS keys.

### Project reflection

This project took me approximately one hour. It was most rewarding to see the success message on the test account after changing the KMS configurations.

I did this project today because I want to learn about all aspects of cybersecurity, including cloud security. This project allowed me to learn more about one of the most important concepts in cybersecurity, the confidentiality of data at rest through encryption.

---

## Encryption and KMS

Encryption is the process of turning plaintext (text anyone can see and read) into ciphertext (text that can only be read by someone with the correct key). Companies and developers do this to ensure the confidentiality of data. Encryption keys are strings of text that are used to encrypt and decrypt data. The strength of a key is correlated to its length.

AWS KMS is a service that can create and manage encryption keys, delegate access to those keys, and encrypt and decrypt data using the keys. Key management systems are important because managing encryption keys can be difficult if you have multiple keys for different resources. Utilizing a KMS can simplify and enhance the security of this process.

Encryption keys are broadly categorized into two categories: symmetric and asymmetric. Symmetric encryption uses one key to encrypt and decrypt data; it's faster than asymmetric, but the drawback is that it's less secure. Asymmetric encryption uses two keys, a public key to encrypt and a private key to decrypt. It's slow but highly secure. I set up a symmetric key because I'm going to be the only person accessing my data.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

My encryption key will safeguard data in DynamoDB, which is data at rest. Data at rest refers to data that is stagnant, usually in a database or a file. Using my KMS, it will encrypt all the data in the columns of the DynamoDB table and only those with access to the key will be able to use it.

The different encryption options in DynamoDB include AWS-owned key, AWS-managed key, and customer-owned key. Their differences are based on the amount of control you have over the key and its use. I selected the customer-owned key so that I can use the key I created with KMS.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

Rather than controlling who has access to the key, KMS checks if the user has the correct permissions to access the data.

Despite encrypting my DynamoDB table, I could still see the table's items because I'm an authorized user for the KMS key. DynamoDB uses transparent data encryption, which means that it checks to see if you're an authorized user for the encryption key, and if you are, it automatically decrypts the data and presents it to you.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I configured a new IAM user to test, and gave them full access to my DynamoDB resources, but not access to KMS resources.

After accessing the DynamoDB table as the test user, I encountered an access denied error message. I encountered this error because the test account does not have permission from KMS to access this resource. This confirmed that my KMS policies are configured correctly.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user access the data in the DynamoDB, I added it as an authorized account in my KMS configuration. My key's policy was updated to allow access to that specific user account.

Using the test user, I attempted to access the items inside the DynamoDB table. I observed that I was successfully able to view the item, which confirmed that my configurations were correctly set up.

Encryption secures data instead of access to the resource. I could combine encryption with roles to allow specific roles to perform tasks while still allowing other users to access the resource.

![Image](http://learn.nextwork.org/intense_azure_festive_sow/uploads/aws-security-kms_feffb2fb8)

---

---
