<a href="https://github.com/alamscode/MySQLApplication/blob/master/MySQLApp.jpg"></a>
# A Simple MySQL Application
> An pplication that performs basic Create and Read operations. Using the AWS platform, the whole infrastructure instructions are written in YAML format in the form of nested stacks. Properly parameterized and mapped, all the stacks can be run in any Region on the AWS platform for the purpose of testing and further development.

## Prerequisites
```
Amazon Web Services Account
Knowledge of AWS resources
```

## Setup
The infrastructure consists of three nested stacks. Each stack is explained in detail as follows:

### VPC
Being the first stack, it includes the resources necessary for setting up a Virtual Private Cloud (VPC). The VPC is completely customizable and consists of all the necessary parameters as shown in picture below.

<a href=""></a>
<a href=""></a>

By default, it spans two availability zones creating one public subnet and one private subnet in one AZ and an other public subnet in the other AZ. The public subnets are connected to the internet through an internet Gateway and and the private subn<a href=""></a>et is connected to the internet through a Nat Gateway that is connected to one of the public subnets. No inbound traffic is allowed to the private subnet, except through the public subnet (this purpose was achieved through necessary security groups).

### Instances
This stack is dependent on the VPC stack. In this stack, an instance is launched (Application Server) in the private subnet. The user data of the instance contains all the necessary commands for installation of the mysql server when it is launched. Since it is in the private subnet, it has no public ip and not accessible through https or ssh publicly.

### AutoScale
This is the last stack. It depends on the 'Instances' stack. It contains the following resources:
- Launch configuration for public instances (Web Server)
- Application Load Balancer for Web Servers
- Classic Load Balancer for Application Server
- AutoScaling groups for Web Server and Application Server

Two web servers will be launched in the public subnets in different availability zones. The web servers will be only accessible through the Application load balancer. 
