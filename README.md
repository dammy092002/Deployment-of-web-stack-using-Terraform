# Terraform

Terraform is a tool for declarative infrastructure as code from Hashicorp. Users define and provide data center infrastructure using a declarative configuration language known as HashiCorp Configuration Language, or optionally JSON.
Terraform is an infrastructure as code (IaC) tool that allows you to build, change, and version infrastructure safely and efficiently. This includes low-level components such as compute instances, storage, and networking, as well as high-level components such as DNS entries, SaaS features, etc. Terraform can manage both existing service providers and custom in-house solutions.

## Project Description and Procedure

This project describes how Terraform was used to build a Web Application on AWS. 

The Reference architecture for this project consists of the following components:

- VPC (Project will be launched in a VPC with both private and public subnets). VPC components like subnets, NAT gateway, Internet Gateway, route tables, Elastic IP, etc will be created.
- Web Servers (Autoscaling group and launch configuration also configured to dictate the number of EC2 instances to be launched per time).
- App Servers (Autoscaling group and launch configuration also configured to dictate the number of EC2 instances to be launched per time).
- 2 ELBs, one for each of the Web Server Group and App Server Group
- MySQL RDS Service (Primary with read replica) Multi-AZ.
- Security Groups for each resource.

All the required terraform codes for all the components of this project have been added in this repository. Some of them are as follows:

(1) provider.tf : This defines the terraform provider for this project, which is AWS. It also defines the variables used to access the AWS cloud environment like the access and secret keys. The AWS region variable to create the resources also defined in this file.

(2) variable.tf : This file defines all the different variables used to define all the resources required in this project. 

(3) terraform.tfvars : This file defines the values for all the different variables used in this project. 

(4) vpc.tf: This file creates all the networking resources in this projects like the vpc, subnets, route tables, Elastic IP, Nat gateway, internet gateway, etc.

(5) rds_instance_production.tf: This file creates the MySQL RDS resources used in this project.

(6) alb_webserver.tf : This creates all the resources for the application load balancer for the frontend web servers.

(7) alb_appserver.tf : This creates all the resources for the application load balancer for the app servers.

(8) asg_launch_config.tf : This creates the launch configuration for both the web and app servers.

(9) asg_webserver.tf : This creates the autoscaling group for the web servers and hence creates the web servers.

(10) asg_webserver.tf : This creates the autoscaling group for the app servers and hence creates the app servers.

(11) sg_*.tf: All the sg* files creates the security groups required for each resources to function appropriately according to the principle of least privilege.

(12) demo_code folder: consists of the bootstrap scripts required to be run on the web and app servers as they come up.




The following procedure was followed to deploy the project.

```python
(1) Run a terraform plan to see how terraform will create all the required resources for this Web application. There are about 31 resources that will be created for this project. The terraform plan output should be successful and show all the components that will be created.

$terraform plan

(2) Run the terraform apply command to create all the resources for this project. Type "yes" to give the go ahead to create the resources once you are satisfied. This will take some time, so be patient with it till all the resources have been created successfully.

$terraform apply


```


#NOTE: 
(1) You need to change the keypair value in the code to your own keypair or else you will get some error.

(2) You need to input your provider information in the provider.tf file.

(3) You need the democode subfolder with bootstrap test scripts



## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
