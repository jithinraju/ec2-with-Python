# Python codes to create and manage ec2 instances

Python can be used for management of Amazon Web Services (AWS) Elastic Compute Cloud (EC2) infrastructure.

You need to install Boto3 library in Python and the AWS Command Line Interface (CLI) first. You can use **pip** tool which is a package management system written in Python used to install and manage packages that can contain code libraries and dependent files

Boto3 = AWS SDK for Python, which provides Object-based APIs and low-level direct access to AWS services like EC2
AWS CLI = command line tool written in Python that introduces efficient use cases to manage AWS services 

```shell

pip install awscli boto3

```

## Create a User and get AWS Access ID

create your user credentials on the AWS console, so that AWS services can be access programmatically. Follow these steps to create your user credentials:

- Launch the Identity and Access Management console (IAM) in AWS. 

- Click Users on the navigation menu on the left of the screen. 

- In the popup window, click on Add User. 

- To set the permissions, choose 'Attach Existing Policies Directly' and in the Policy Filter type 'AmazonEC2FullAccess' and then click the 'next' button. 

- Review the user and permission levels, and click on the 'Create User' button. 

- The next page will show your keys which is only available once, so download and save then safely in a secure location. 

## Configure AWS Credentials Locally

Use the AWS CLI tool to configure User credentials by running the following command from a Bash terminal.

```bash

aws configure

```

This will prompt you to provide the Access Key ID, Secret Key, Default AWS region, and output format. These credentials are saved in a local file at path ~/.aws/credentials and other configurations like region are stored in ~/.aws/config file


## Create Key Pair for EC2 Instance

Need to create a keypair for EC2 instances, so that they can be accessed later.

```python

import boto3
ec2 = boto3.resource('ec2')

# create a file to store the key locally

Keyfile = open('ec2-keypair.pem','w')

# call the boto ec2 function to create a key pair

key_pair = ec2.create_key_pair(KeyName='ec2-keypair')

# capture the key and store it in a file

KeyPairOut = str(key_pair.key_material)
print(KeyPairOut)
Keyfile.write(KeyPairOut)
Keyfile.close()

```

The above program not only creates a key pair in AWS, it also captures and stores it on your local machine. You can use this key pair to SSH into the virtual machines later. Please make sure to change the mode of the key pair file to read-only using the following command in bash terminal


```bash

chmod 400 ec2-keypair.pem

```


## Create a New EC2 Instance

You need to find the Amazon Machine Image (AMI) ID which is required to create a new instance 

Run the following command from a Bash shell: 

```bash

aws ec2 describe-instances

```
This should return details of any EC2 instance running on AWS in JSON format and you can also obtain the AMI ID from the AWS console in your browser when you launch and instance. 

```python

import boto3
ec2 = boto3.resource('ec2')

# create a new EC2 instance
instances = ec2.create_instances(
     ImageId='ami-0d8f6eb4f641ef691',
     MinCount=1,
     MaxCount=2,
     InstanceType='t2.micro',
     KeyName='ec2-keypair'
 )

```

- ImageID = Amazon Machine Image (AMI) ID 
- MinCount and MaxCount = number of EC2 instances to launch
- InstanceType = size of the instance (t2.micro, t2.small, or m5.large)
- KeyName = name of the key pair that will allow access to the instance

After running the above script, EC2 instance will be deployed in your EC2 dashboard in AWS console
