

# Encrypt Data with AWS KMS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-kms)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_w0x1y2z3)

---

## Introducing Today's Project!

In this project, I’ll demonstrate how to secure data using encryption. The goal is to create encryption keys with AWS KMS (Key Management Service), use those keys to encrypt data in a DynamoDB table, and then test access control using different IAM users.

### Tools and concepts

Services I used include AWS KMS ( Key Management Service ), DynamoDB, AWS IAM. Key concepts I learned include encryption, database tables, KMS using permission to actions rather than just access to the key itself, creating a user to test access.

### Project reflection

Completing this project took me around 3 hours, including research, testing, and implementation. The most challenging yet rewarding aspect was diving deep into encryption mechanisms and understanding how they differ from traditional access control tools.

Breaking down complex concepts and successfully implementing encryption for secure user access was incredibly fulfilling. Seeing the test user securely gain encrypted access validated the effort and deepened my interest in Cloud Security.

I took on this project to deepen my hands-on understanding of encryption and data security in real-world applications. While theoretical knowledge is essential, I wanted to see firsthand how tools like AWS KMS integrate with databases and user access controll critical skills for modern cloud security.

The project exceeded my goals: not only did it solidify my grasp of encryption principles, but it also gave me practical experience in implementing secure systems. 
Seeing AWS KMS seamlessly manage keys and permissions reinforced how powerful and necessar these solutions are in protecting sensitive data.


---

## Encryption and KMS

Encryption is the process of converting plain, readable data into a secure, unreadable format to protect it from unauthorized access. It uses encryption keys, which guide the algorithm on how to encrypt and decrypt the data.



AWS KMS (Key Management Service) is a secure vault for managing encryption keys. It helps protect and control access to the keys used to encrypt data. If someone gains unauthorized access to those keys, they could decrypt sensitive data making key security critical to overall data protection.



I chose a symmetric key because it uses the same key for both encryption and decryption, making it faster and more efficient for securing data at rest, like in a DynamoDB table. It's ideal for internal applications where key access can be tightly controlled.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_a2b3c4d5)

---

## Encrypting Data

Amazon DynamoDB is a fully managed, fast, and flexible NoSQL database service from AWS. It’s designed for applications that need low-latency access to large volumes of data, making it ideal for use cases like gaming, IoT, mobile apps, and real-time analytics.

In this project, I’m using DynamoDB to store data and securing it with an encryption key from AWS KMS to ensure it's protected against unauthorized access.

DynamoDB offers three encryption options:
-DynamoDB owned key, Fully managed by AWS, with no visibility or control.
-AWS managed key, AWS creates and manages the key, but we get limited visibility.
-Customer managed key (CMK), I create and manage the key using AWS KMS, offering full control and monitoring.

For this project, I selected (CMK) to use the KMS key I created earlier, giving me greater security oversight.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_q8r9s0t1)

---

## Data Visibility

KMS doesn’t just control who can see the key it controls what actions users can perform with it. For example, even if a user can view the key, they still need explicit permissions to use it for decryption. This ensures fine-grained access control over sensitive data.



Even though the DynamoDB table is encrypted, I can still view its items because I’m an authorized user of the encryption key. DynamoDB uses transparent data encryption, which automatically encrypts and decrypts data for authorized users without changing how we access it.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_c0d1e2f3)

---

## Denying Access

I created a new IAM user to test access restrictions on encrypted data. This user was granted full access to DynamoDB, but no permissions to encrypt or decrypt using AWS KMS. This setup helps validate that the encryption key properly restricts unauthorized access.

When accessing the DynamoDB table as the test IAM user, I received an Access Denied Exception. This confirmed that, without decryption permissions, the user could not view the data, proving that the encryption key effectively secures sensitive information.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_w0x1y2z3)

---

## EXTRA: Granting Access

To let my test user use the encryption key, I made it a key user in the  KMS console. My key's policy was updated to allow th nextwork-kms-user to encrypt, decrypt, re-encrypt etc using the key.

I logged in as the test user and retried accessing the DynamoDB table. This time, the user could view the data, confirming that assigning the proper KMS permissions successfully authorized access to the encrypted content.

Encryption secures data instead of an entire resource or service. I could combine encryption with others access control tools like (security groups and permission policies) to have two layers of security :
- The resource level.
- The data level.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-security-kms_feffb2fb8)

---

---
