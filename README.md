# AWS-S3
## Repository for the work done on AWS S3
## What is S3?
S3 is a simple storage service. A database available on AWS. It's available globally and you can store anything. Used for disaster recovery (DR). We can apply Create bucket/object , read,update and delete (CRUD) actions. If there were a disaster in the location where our instances are located (Ireland for us) we would lose a lot of work.So we need to back them up. We need AWS SEC and ACCESS KEYs to access the S3. 

Log into the AWS console, and then install python 3.
Make sure that you install python 3 and use an alias for it to make the problem easier. Input `sudo pip3 install AWSCLI` and install.

When you get to the right part type `AWS configure` into your console and input your access and security keys. WARNING: these keys are extremely important and shouldn't be put anywhere that could lead to them being compromised. Be careful. Make sure the region is eu-west-1a and language is json. If this is all done correctly you should be able to access the S3. type ls to check.

![S3 recovery](https://user-images.githubusercontent.com/39882040/152983543-0aecf326-9fd6-46a3-9ce3-f8cdbe86514a.PNG)

S3 storage classes:

- standard: You can access data anytime, general purpose.
- Glacier: infrequent data access(pay less), longterm retention of data
- Infrequent access: Made primarily for disaster recovery files because of the low cost and high durability
- see https://aws.amazon.com/s3/storage-classes/ for more examples

### Creating an S3 bucket
Don't use underscore or caps when creating the bucket. In order to create a on AWS follow these instructions:
- To make sure you're in the s3 type the command `aws s3 ls`
- enter this command into git bash `aws s3 mb s3://eng103-name-devops`. If successful it should return make bucket and the name that has been given to it.
- `sudo nano test.txt` to create a file
-  `aws s3 cp test.txt s3://eng103a-name-devops` to upload the file to bucket

This will create and upload an onject. Make sure to go to permisissions and allow public access.

- `sudo rm test.txt` to delete the file locally
- `aws s3 cp s3://eng103a-name-devops/test.txt ~` to download a file called test.txt over from the s3
- `aws s3 rb s3://eng103a-name-devops` to delete a bucket if it is empty. If it has anything in it, it will fail
- `aws s3 rm s3://eng103a-name-devops` to delete files in a bucket
- `aws s3 rm s3://eng103a-name-devops --recursive` delete all content files. WARNING:don't use if you have a lot of files. It will delete everything.

These are all the CRUD methods.
# Automating the CRUD methods using python scripting
In order to automate the CRUD methods we need to use python scripting. This means running python scripts in a terminal. We need to install python 3 for the terminal. This can be done quite easily, using `sudo install python3`. 

```
#!/usr/bin/env python3

import boto3

filename = 'test.txt'
bucket_name = 'eng103a-frederick-devops'
location = {'LocationContraint':'eu-west-1'}

s3 = boto3.resource('s3'
s3.create_bucket(Bucket=bucket_name, CreateBucketConfiguration=location)
s3_client = boo3.client('s3')
s3_client.upload_file(filename,bucket_name,filename)

s3 = boto3.client('s3')
s3.download_file('eng103a-frederick-devops','test.txt','test2.txt')

s3 = boto3.resource('s3')
s3.object('eng103a-frederick-devops','test.txt').delete()

s3 = boto3.resource('s3')
bucket = s3.Bucket('eng103a-frederick-devops')
bucket.delete()

```
This piece of code does the CRUD parts individually and is the piece of code I made. It's a work in progress because I need to include a while loop if I want to do it in one .py file. I took inspiration from a classmate's code, I spoke to him about the code and I believe I understand it.
```
import boto3
location = {'LocationConstraint': "eu-west-1"}
s3 = boto3.resource('s3')
bucket_name = 'eng103a-frederick-devops'

while True:
    action = input("what would you like you to do? c for createbucket, db for delete bucket, d for delete file, u for upload, dl for download, e for exit\n").lower()

    if action == "db":
        s3.Bucket(bucket_name).delete()
    elif action == "cb":
        s3.create_bucket(Bucket=bucket_name, CreateBucketConfiguration=location)
    elif action == "d":
        filename = input("what is the filename?\n")
        s3.Object(bucket_name, filename).delete()
    elif action == "u":
        filename = input("what is the name of the file you're uploading?\n")
        targetfilename = input("what is the destination file name?\n")
        s3.Bucket(bucket_name).upload_file(filename, targetfilename)
    elif action == "dl":
        filename = input("what is the name of the file you're downloading?\n")
        targetfilename = input("what is the destination file name?\n")
        s3.Bucket(bucket_name).download_file(filename, targetfilename)
    elif action == "e":
        break
```
<<<<<<< HEAD
# AWS Autoscaling load balancing
High availabilty- Able to replicate instances so if an instance goes down, then it won't effect the app
High scalability- 
Deployed in multi AZs

Autoscaling automatically adjusts the amount of computational resourcs based on server load.
Load Balancing distributes traffic between EC2 so that no one instance gets overwhelmed.
An ALB application gets information from the internet gateway and distributes the load according to the instances. If one instance goes down the ALB will distribute the load to a new instance and boot up a new instance.

In order to get this to work, we need to create an autoscaling policy (min = 2, desired = 2, max = 3). An example of this in real life is christmas shopping. More demand in December but less in January.

The load balancer listening on port 80 or required ports. Target group - 
=======
![image](https://user-images.githubusercontent.com/39882040/153221617-4d439bbb-8eff-44fd-ada2-6868ab274cca.png)
>>>>>>> 219d5617c206a4f6e33e8594b072ef881e4103cf
