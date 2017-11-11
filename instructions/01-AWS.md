# AWS

## Pre-Requisites

- an AWS account

## Setup AWS instances

We are going to create EC2 instances using the latest Ubuntu Server as OS.

###Select instance

Go to AWS Console, choose the EC2 service. On the EC2 Dashboard, click on **Launch Instance**. You can check *Free tier only* if you like. In the list select the latest Ubuntu Server. Currently, it's 16.04 LTS.

![01-AWS-01](img/01-AWS-01.png)

### Instance type

Choose the **t2.micro** instance type. It is enough for our purposes at the moment. Click on *Next: Configure Instance Details*.

Change the number of instance to 4 and choose a subnet. The last option is useful if we want to scale manually our cluster later. Leave others options as they are. Click on *Next: Add Storage*.

![01-AWS-02](img/01-AWS-02.png)

### Storage

Default is 8Gb, and it's fine for our purpose at the moment. We can increase the size of the EBS volume later so that's ok.

Also don't forget to uncheck **Delete on Termination** as we want to keep our data after stopping our EC2 instances.

![01-AWS-03](img/01-AWS-03.png)

Click on *Next: Add Tags*.

### Tags

A tag allows to identify an instance with a name. Click *Add Tag*, set the **Key** to *Name* and **Value** to *Hadoop*. We will use this tag to re-label our instances later on. 

Click on *Next: Configure Security Group*.

### Security Group

This step lets us define rules regarding the incoming or outgoing access of the instances.

Select *Create a new security group* name it as you like (eg: *HadoopSecurityGroup*) and give it a useful description. For the purpose of testing, we are going to open everything to avoid network errors. Configure as the following image:

![01-AWS-04](img/01-AWS-04.png)

*todo: configure the security group with restricting rules*

Finally, click on *Review and Launch*.

Review the information again and click *Launch* to start the instances. 

## Key pair

We need to create a key pair in order to connect to our instances securely, here throught SSH.

Select *Create a new key pair* from the first dropbox, give a name to the key pair (eg: *hadoopec2cluster*) and download it. As mentioned on the AWS Console, we will not be able to download the file again after it's created, so save it in a secure location. You can store it in the **keys** folder of this repository, it will not be committed.

Click on *Launch*. On the next page, you can directly click on *View Instances* where we are going to rename our instances.

### Renaming

Rename the instances as follow:

- HadoopNameNode (Master)
- HadoopDataNode1 (Slave #1)
- HadoopDataNode2 (Slave #2)
- HaddopDataNode3 (Slave #3)

## SSH configuration

*todo*