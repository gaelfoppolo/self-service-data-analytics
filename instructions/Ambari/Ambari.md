# Ambari on AWS

How to install Ambari on AWS and deploy/manage your Hadoop cluster.

## Pre-Requisites

- 01-AWS completed
- OpenSSH installed or any SSH client

## What will we do?

First we are going to create the Ambari server, that will manage the cluster, and install the components for us. Then we will create a template of slave, that we will replicate and where we will install the components.

## What will we need?

To start small, we will need **6 EC2 instances**, running **Ubuntu Server 16.04 LTS**. Don't create them now, but keep this table for future reference.

|     Purpose     |   Type    | Storage |
| :-------------: | :-------: | :-----: |
|     Ambari      | t2.medium |  15Gb   |
|     Master      | t2.medium |  15Gb   |
| SecondaryMaster | t2.medium |  15Gb   |
|    DataNode1    | t2.small  |  15Gb   |
|    DataNode2    | t2.small  |  15Gb   |
|    DataNode3    | t2.small  |  15Gb   |

## Ambari Server

Create the instance, according to the specs in the table. SSH into it and run the following commands:

```sh
# add the repo & update
sudo wget -O /etc/apt/sources.list.d/ambari.list http://public-repo-1.hortonworks.com/ambari/ubuntu16/2.x/updates/2.5.1.0/ambari.list
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD
sudo apt-get update
# install the server
sudo apt-get install ambari-server
```

Confirm the download. Then launch the setup with:

```sh
sudo ambari-server setup
```

| Question                                 | Response |
| ---------------------------------------- | -------- |
| Customize user account for ambari-server daemon | N        |
| Enter choice                             | 1        |
| License                                  | Y        |
| Enter advanced database configuration    | N        |

Finally launch the server with:

```sh
sudo ambari-server start
```

Wait that the launch complete. Then, you can go to the web interface: `<public DNS>:8080`

## The clients

We are going to create a template instance, that we can replicate, and dodge the painless initial setup for each client.

First, create an instance, with the type you want (eg:  t2.micro), running **Ubuntu Server 16.04 LTS**.

SSH into it and run the following commands:

```sh
# add the repo & update
sudo wget -O /etc/apt/sources.list.d/ambari.list http://public-repo-1.hortonworks.com/ambari/ubuntu16/2.x/updates/2.5.1.0/ambari.list
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com B9733A7A07513CAD
sudo apt-get update
# install the agent
sudo apt-get install ambari-agent
# install ntp and configure it
sudo apt-get install ntp
sudo update-rc.d ntp defaults
sudo update-rc.d ntp enable
sudo /etc/init.d/ntp start
```

We now have our template. Let's create an image of this template.

Back on AWS Console, in the list of instances, select the one we just configure (our template), right-click on it and select **Create an image**.

![create-image](img/create-image.png)

Give an distinguish name and description to your instance and click **Create Image**. You can see your AMI (Amazon Machine Image) just like instances by clicking to **AMIs** on the left menu.

![ami-menu](img/ami-menu.png)

Wait until the status of your image is **available**.

Then create a new instance by selecting the AMI and click **Launch**. You can also create the instance from the EC2 instances list.

According to the specs in the table, create the instances we need (2 master and 3 data nodes).

Do not forget to remove the instance template. You should have something like this:

![list-instances](img/list-instances.png)

We have all our nodes, we can now begin the real install!

## Install the cluster

todo

##Test Hadoop

sudo su

sudo hfs

`/usr/hdp/2.6.3.0-235/hadoop-mapreduce`

`hadoop jar /usr/hdp/2.6.3.0-235/hadoop-mapreduce/hadoop-mapreduce-examples-2.7.3.2.6.3.0-235.jar pi 15 1000`