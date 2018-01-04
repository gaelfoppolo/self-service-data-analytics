# Complete install

This document contains the information used for the install of a cluster with every services we choose for our architecture. We assume you are familiar with Ambari interface.

## Nodes list

We will need **8 EC2 instances**, running **Ubuntu Server 16.04 LTS**.

|   Name    |                 Purpose                  |   Type    | Storage |
| :-------: | :--------------------------------------: | :-------: | ------- |
|  Ambari   |              Ambari Server               | t2.medium | 15Gb    |
| Master #1 |         Name Node + Spark Server         | t2.large  | 15Gb    |
| Master #2 | Secondary Name Node + YARN + Map Reduce  | t2.large  | 15Gb    |
| Master #3 | Hive Server + Oozie Server + Atlas Server + HBase Master + Knox | t2.large  | 15Gb    |
| Master #4 |                Hue Server                | t2.medium | 15Gb    |
| Client #1 | Data Node + Node Manager + Flume + HBase +  Spark | t2.medium | 15Gb    |
| Client #2 | Data Node + Node Manager + Flume + HBase + Spark + Spark2 | t2.medium | 15Gb    |
| Client #3 | Data Node + Node Manager + Flume + HBase +  Spark2 | t2.medium | 15Gb    |

## Services list

Select the following services:

- HDFS
- YARN + MapReduce2
- Tez
- Hive
- HBase
- Pig
- Sqoop
- Oozie
- ZooKeeper
- Flume
- Ambari Infra
- Ambari Metrics
- Atlas
- Kafka
- Knox
- SmartSense
- Spark
- Spark2
- Hue
  - if not available, please follow this guide to add it to your Ambari
- Slider

## Masters assignations list

Split the following services on the masters instances. We can review this assignment if needed in the future.

|            Services            |   Where   |
| :----------------------------: | :-------: |
|        NameNode (HDFS)         | Master #1 |
|        SNameNode (HDFS)        | Master #2 |
|   App Timeline Server (YARN)   | Master #2 |
|     ResourceManager (YARN)     | Master #2 |
|   History Server (MapReduce)   | Master #2 |
|  ZooKeeper Server (ZooKeeper)  | Master #1 |
|  ZooKeeper Server (ZooKeeper)  | Master #2 |
|  ZooKeeper Server (ZooKeeper)  | Master #3 |
|  Infra Solr Instance (Ambari)  | Master #1 |
|   Metrics Collector (Ambari)   | Master #2 |
|        Grafana (Ambari)        | Master #2 |
| Activity Analyzer (SmartSense) | Master #1 |
| Activity Explorer (SmartSense) | Master #1 |
| Spark2 History Server (Spark2) | Master #1 |
|  Spark History Server (Spark)  | Master #1 |
|    HST Server (SmartSense)     | Master #1 |
|        Hue Server (Hue)        | Master #4 |
|     Hive Metastore (Hive)      | Master #3 |
|     WebHCat Server (Hive)      | Master #3 |
|      HiverServer2 (Hive)       | Master #3 |
|      HBase Master (HBase)      | Master #3 |
|      Oozie Server (Oozie)      | Master #3 |
| Atlas Metadata Server (Atlas)  | Master #3 |
|      Kafka Boker (Kafka)       | Master #3 |
|      Knox Gateway (Knox)       | Master #3 |

## Slaves assignations list

todo

## Customize services list

Some services need require information from us, in order to work properly.

- [Hive](../Hive/ambari_install_customize.md)
- [Oozie](../Oozie/ambari_install_customize.md)
- [Knox](../Knox/ambari_install_customize.md)
- [SmartSense](../SmartSense/ambari_install_customize.md)

The others services are good with the default parameters, but can also need some custom. Please edit this part if further custom of these services is needed.