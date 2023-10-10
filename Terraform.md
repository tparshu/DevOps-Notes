Terraform
--------------------
WHats is Terraform ?
It is Infrastructure as code ( IAC ) tool.
It is an open-source tool created by  HashiCorp in 2014.


List IAC  tools which are popular
------------------------------------
1) Terraform
2) CloudFormation
3) Heat
4) Ansible
5) SaltStack

Ansible is primary known as Configuration Management tool, to an extent it can also create Infrastructure.
 

Terraform support multiple providers.

Examples of providers are
1) AWS
2) Azure
3) GCP
4) Oracle Cloud
5) Alibaba Cloud
6) VMware
and many more

To look at list of providers, use the below link
https://registry.terraform.io/browse/providers

--------------------------------------------------------------
Installation of terraform
-------------------------------

Installation of terraform is simple.

Step 1:  Search for "Terraform download" in google
Take the link from the site terraform.io

as my laptop is windows 64 bit OS

download Amd64

Zip file gets downloaded.

Zip file contains only one file, ie   terraform.exe

Lets extract this terraform.exe in desktop.
Now, the terraform.exe is available in desktop.

Lets open the command prompt, point to the desktop


C:\Users\ADMIN\Desktop>terraform
We get the list of commands.

ThatsAll!!! Folks
Terraform installation is completed.


If you run the terrafrom cmd in any other location, it will not work.

So, lets create a new folder in E: drive with the name sunil

E:\sunil
Lets copy terraform.exe file in the D:\tushar

Mention the path E:\sunil  in path environment variable. 

ThatsAll,
Terraform works from any location.

---------------------------
Working with IDE

I recommend to use ATOM editor for writing terraform code.

URL -  https://atom.io/

Download the editor ( exe file )
Run the editor.

language-terraform package to be installed in the editor.

Open the editor ---> Install a package --- Open Installer


Mention the package "language-terraform"
install.


Add the project folder  in the atom editor.


Creating EC2 Machine using terraform
Points to be considered

1. In which AWS Account ( Authentication ), the EC2 Machine should be created?
2. In which region?
3. Which resource  ?

Go to terraform registry  (   )

Browse providers --->  AWS ---> Documentation



Lets create IAM user
Provide CLI Access,'
and Attach administratorAccess to the user.

Username - user1




Lets Authenticate using access-key-id and  Secret Access Key

Access Key ID: AKIAS4ED5DEIA36D7XMO

Secret Access Key: 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


In the ATOM editor,
Lets create a new file in the project
ll_ec2.tf


Goto Documentation

# Configure the AWS Provider
provider "aws" {
  region = "us-east-1"
}



Under Authentication and Configuration


provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}


As authentication is completed.
Lets create EC2 resource


Search for EC2 -----> aws_instance


Check this code

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"

}


aws_instance -- refers to EC2 Machine
web  -- refers to the name of the instance

Ex:

provider "aws" {
  region = "ap-south-1"
  access_key = "AKIA4RZPP3FZW53FHWOH"
  secret_key = "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"
}

resource "aws_instance" "pavan" {
  ami           = "ami-07eaf27c7c4a884cf"
  instance_type = "t2.micro"
}



Now, lets open the terminal

Lets point to the directory, where the terraform file is availble

C:\Users\ADMIN\Desktop\devops530> terraform init

This command will download the AWS related plugins

Next command to run

> terraform plan

It tells you, what terraform is planning to create.

Next command to run
>  terraform apply


It will ask you enter a value
yes   --- if you want to create.
no    ---  if you do not want to create.

Done!!!! 
We have created infrastructure using the code.

code
-------------

provider "aws" {
  region = "ap-south-1"
  access_key = "AKIA4RZPP3FZW53FHWOH"
  secret_key = "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"
}

resource "aws_instance" "pavan" {
  ami           = "ami-04893cdb768d0f9ee"
  instance_type = "t2.micro"
}



