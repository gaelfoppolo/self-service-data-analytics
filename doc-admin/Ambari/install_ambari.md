# Install Ambari

How to install Ambari on AWS and deploy/manage your Hadoop cluster.

## Pre-Requisites

- To know how to launch & config EC2 instances
- OpenSSH installed or any SSH client

## What will we do?

First we are going to create the instances we need. Then we will launch the install and config the components.

## What will we need?

To start small, we will need **6 EC2 instances**, running **Ubuntu Server 16.04 LTS**. Don't create them now, but keep this table for future reference.

|     Purpose     |   Type    | Storage |
| :-------------: | :-------: | :-----: |
|  Ambari Server  | t2.medium |  15Gb   |
|     Master      | t2.medium |  15Gb   |
| SecondaryMaster | t2.medium |  15Gb   |
|    DataNode1    | t2.small  |  15Gb   |
|    DataNode2    | t2.small  |  15Gb   |
|    DataNode3    | t2.small  |  15Gb   |

## Create cluster

Report to the document [_Create templates_](./create_templates.md) to create the server and the client template.

Then, according to the specs in the table, create the instances we need (1 server, 2 master, 3 data nodes).

You should have something like this:

![list-instances](img/list-instances.png)

We have all our nodes, we can now begin the real install!

## Install the cluster

In this part, we are only going to use the browser, we are done with the terminal.

We can access the Ambari Install Wizard through the browser, to `http://<public DNS of your Ambari server>`.

We should now be on the login page of Ambari Server. Log in using the default username/password: **admin/admin**. We can change this later to whatever we wish.

![ambari-wizard](img/ambari-wizard.png)

Click **Launch Install Wizard**.

Choose the name of your cluster.

On the next page, **Select Version**, no need to modify anything, simply go **Next**.

On **Install Options**, we need to fill a couple of information:

- Target Hosts: enter the **private DNS** of each slave nodes, one per line
- Host Registration Information: select the private key (`id_rsa`) we downloaded before.
- SSH User Account: change to `ubuntu`

![ambari-install-options](img/ambari-install-options.png)

Click **Register and Confirm** to continue.

Wait during the registering process. At a couple of minutes, the status of all host should be **Success**. Click **Next**.

### Services

On the next page, we choose the services we want to install in our cluster. Don't worry we will be able to add new service after initial setup. For starter, only select the following services:

- HDFS
- YARN + MapReduce2
- ZooKeeper
- Ambari Infra
- Ambari Metrics

Click **Next** to confirm the selection.

### Master

On the next page, we assign master components to hosts you want to run them on.

I recommand to split on the two masters instances (Master and SecondaryMaster) first. We can review this assignment if needed in the future.

|          Services          |      Where      |
| :------------------------: | :-------------: |
|         SNameNode          | SecondaryMaster |
|          NameNode          |     Master      |
| App Timeline Server (YARN) |     Master      |
|      ResourceManager       |     Master      |
| History Server (MapReduce) |     Master      |
|      ZooKeeper Server      |     Master      |
|    Infra Solr Instance     | SecondaryMaster |
|     Metrics Collector      | SecondaryMaster |
|          Grafana           | SecondaryMaster |
|     Activity Analyzer      | SecondaryMaster |
|     Activity Explorer      | SecondaryMaster |
|         HST Server         | SecondaryMaster |

When you are satisfied with the assignments, choose **Next**.

### Slaves

On the next page, we assign slave components to hosts you want to run them on.

I recommand to install on the three instances that we choose to be our data nodes (without the *✵* in the list):

- DataNode
- NodeManager
- Client

Click **Next** to continue.

### Customize Services

This step presents a set of tabs that let us review and modify the cluster setup. It attempts to set reasonable defaults for each of the options.

**Any tab that requires input shows a red badge with the number of properties that need attention.**

At the moment, only two services need some information from us: Ambari Metrics and SmartSense.

The tabs needing our attention, are demanding the default password of the admin account, to access this service. You can go with **admin** for both of us.

![ambari-services-custom](img/ambari-services-custom.png)

The others services are good with the default parameters, but can also need some custom. Please edit this part if further custom of these services is needed.

Click **Next** to continue.

### Review & install

On the next page, we can review our installation before actually doing the install. If everything looks good to you, click **Deploy**!

The progress of the install displays on the screen. Ambari installs, starts, and runs a simple test on each component. Overall status of the process displays in progress bar at the top of the screen and host-by-host status displays in the main section. **Do not refresh your browser during this process. Refreshing the browser may interrupt the progress indicators.**

![ambari-deploy](img/ambari-deploy.png)

When `Successfully installed and started the services` appears, choose **Next**.

On the next page, we get a summary of the deployment. Hit **Complete** to land on Ambari main page, showing metrics and global status of services!

![ambari-metrics](img/ambari-metrics.png)

## Autostart of services

We can configure Ambari to autostart the services automatically when started.

In Ambari web interface, go to **Admin** > **Service auto start**.

Simply **Enable all** component for each service and **Save**.

Now, when you will start your instances, Ambari will automatically boot all the services for you :tada:

## Where to go?

Report to the document [_Let's test Hadoop!_](./hadoop_test.md) to test your cluster installation.

*todo: add new services*