# Terraform-Lab






Lab 1 and 2: 
How to create a VPC and subnet in AWS using Terraform?
Step 1: Create an IAM 
	In the search type IAM, then select add user and give a name and select pragmatic access for secret key id and secret access key

	 



Step 2: Permission: Select attach existing policies directly and choose AdministratorAccess


 



Step 3: Review and create user

 


Step 4:  Download .csv file that has Access key ID and Secret accesskey in the same computer


 
======================================================
In the terminal:
 
	which terraform shows the path of terraform : /user/local/bin/terraform
Open the VS Code: In the terminal
cd Desktop/

Make a folder:
mkdir tfexamples
Make a file in it: 
touch provider.tf

terraform plan
terraform init
terraform apply





 


=====================================================================

Lab 2:

How to create a subnet in AWS using Terraform?

resource "aws_subnet" "subnet1" {		//Type of resource
  vpc_id     = “${aws_vpc.main.id}”        //Type of resource. Logical name.vpc id
  cidr_block = "190.160.1.0/24"

  tags = {
    Name = "subnet1"
  }
}

Note: Then check the aws, vpc and subnet is created.
===========================================================

Lab 3:
AWS S3 bucket from terraform
 

In the terminal:
terraform apply

Then it will create bucket in aws. Check aws:
 
AWS Simple Storage Service (S3) provides secure, durable and highly scalable object storage. S3 is easy to use and we can store and retrieve any amount of data from anywhere on the web.

versioning: Versioning automatically keeps up with different versions of the same object.
NOTE: Every S3 bucket must be unique and that why random id is useful to prevent our bucket to collide with others.
=====================================================================
LifeCycle Management
Why do we need LifeCycle Management?
•	To save cost
•	In most of the cases, data which is generated by our application is relevant for us for the first 30 days and after that, we don't access that data as frequently.

\LifeCycle object supports the following but I am going to enable just the required parameters
•	enabled — (Required) Specifies lifecycle rule status.
•	transition - (Optional) Specifies a period in the object's transitions

provider "aws" {
  region = "us-west-2"
}
resource "aws_s3_bucket" "bucket" {
  bucket = "terraform-20181219040316452900000001"
  acl = "private"

  lifecycle_rule {
    enabled = true

    transition {
      days = 30
      storage_class = "STANDARD_IA"
    }

    transition {
      days = 60
      storage_class = "GLACIER"
    }
  }
}
•	Here I am defining after 30 days move the objects to STANDARD_IA and after 60 days to GLACIER.
==================================================================

Lab 4: 

 Create an EC2 and install docker (use the user_data) : Though it doesn’t work

Needs: AMI

 













Note: You need to install aws cli and terraform
For macOs:
curl “https://awscli.amazonaws.com/AWSCLIV2.pkg” -o “AWSCLIV2.pkg”
sudo installer -pkg AWSCLIV2.pkg -target /

Terraform install for MacOs:
$ brew tap hashicorp/tap
$ brew install hashicorp/tap/terraform
$ brew upgrade hashicorp/tap/terraform
$ terraform -install-autocomplete
	Check the version terraform –version



	Resources:

	https://medium.com/avmconsulting-blog/how-to-deploy-a-dockerised-node-js-application-on-aws-ecs-with-terraform-3e6bceb48785

	https://www.youtube.com/watch?v=IxA1IPypzHs      [ how to create VPC and Subnets in aws using Terraform]

	https://medium.com/appgambit/terraform-aws-vpc-with-private-public-subnets-with-nat-4094ad2ab331
	https://medium.com/faun/aws-s3-bucket-using-terraform-fb2e36c85d8a

