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

### Creating an S3 bucket
Don't use underscore or caps when creating the bucket


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