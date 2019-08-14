# Python codes to create and manage ec2 instances

Python can be used for management of Amazon Web Services (AWS) Elastic Compute Cloud (EC2) infrastructure.

You need to install Boto3 library in Python and the AWS Command Line Interface (CLI) first. You can use **pip** tool which is a package management system written in Python used to install and manage packages that can contain code libraries and dependent files

Boto3 = AWS SDK for Python, which provides Object-based APIs and low-level direct access to AWS services like EC2
AWS CLI = command line tool written in Python that introduces efficient use cases to manage AWS services 

```shell

pip install awscli boto3

```

# Create a User and get AWS Access ID

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

