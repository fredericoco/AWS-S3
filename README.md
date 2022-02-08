# AWS-S3
## Repository for the work done on AWS S3
## What is S3?
S3 is a simple storage service. A database available on AWS. It's available globally and you can store anything. Used for disaster recovery (DR). We can apply Create bucket/object , read,update and delete (CRUD) actions. If there were a disaster in the location where our instances are located (Ireland for us) we would lose a lot of work.So we need to back them up. We need AWS SEC and ACCESS KEYs to access the S3. 

Log into the AWS console, and then install python 3.
Make sure that you install python 3 and use an alias for it to make the problem easier. Input `sudo pip3 install AWSCLI` and install.

When you get to the right part type `AWS configure` into your console and input your access and security keys. WARNING: these keys are extremely important and shouldn't be put anywhere that could lead to them being compromised. Be careful. Make sure the region is eu-west-1a and language is json. If this is all done correctly you should be able to access the S3. type ls to check.

![S3 recovery](https://user-images.githubusercontent.com/39882040/152983543-0aecf326-9fd6-46a3-9ce3-f8cdbe86514a.PNG)

S3 storage classes:

standard: You can access data anytime
Glacier: infrequent data access(pay less)
research rest in own time

