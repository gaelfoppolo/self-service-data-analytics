# Configuration 1: small install

This document contains the information used for the install of a cluster with the minimum of services. This way you can familiarize with Ambari.

## Nodes list

We will need **6 EC2 instances**, running **Ubuntu Server 16.04 LTS**.

|     Purpose     |   Type    | Storage |
| :-------------: | :-------: | :-----: |
|  Ambari Server  | t2.medium |  15Gb   |
|     Master      | t2.medium |  15Gb   |
| SecondaryMaster | t2.medium |  15Gb   |
|    DataNode1    | t2.small  |  15Gb   |
|    DataNode2    | t2.small  |  15Gb   |
|    DataNode3    | t2.small  |  15Gb   |

## Services list

Only select the following services:

- HDFS
- YARN + MapReduce2
- ZooKeeper
- Ambari Infra
- Ambari Metrics

## Masters assignations list

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

## Slaves assignations list

I recommand to install on the three instances that we choose to be our data nodes (without the *✵* in the list):

- DataNode
- NodeManager
- Client

## Customize services list

At the moment, only two services need some information from us: Ambari Metrics and SmartSense.

The tabs needing our attention, are demanding the default password of the admin account, to access this service. You can go with **admin** for both of us.

![ambari-services-custom](img/ambari-services-custom.png)

The others services are good with the default parameters, but can also need some custom. Please edit this part if further custom of these services is needed.