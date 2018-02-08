# Complete install

This document contains the information used for the install of a cluster with every services we choose for our architecture. We assume you are familiar with Ambari interface.

## Nodes list

We will need **13 EC2 instances**, running **Ubuntu Server 16.04 LTS**.

|   Name    |                     Purpose                      |   Type    | Storage |
| :-------: | :----------------------------------------------: | :-------: | ------- |
|  Ambari   |                  Ambari Server                   | t2.medium | 15Gb    |
| Master #1 |              Name Node + ZooKeeper               | t2.medium | 15Gb    |
| Master #2 | Secondary Name Node + ZooKeeper + Ambari Metrics | t2.medium | 15Gb    |
| Master #3 |          YARN + Map Reduce + ZooKeeper           | t2.medium | 15Gb    |
| Master #4 |           Spark + Spark 2 + SmartSense           | t2.medium | 15Gb    |
| Master #5 |               Hive + Oozie + HBase               | t2.medium | 15Gb    |
| Master #6 |                       Knox                       | t2.medium | 15Gb    |
| Master #7 |                  Atlas + Kafka                   | t2.medium | 15Gb    |
| Master #8 |                       Hue                        | t2.medium | 15Gb    |
| Client #1 |     Data Node + Node Manager + Flume + HBase     | t2.large  | 40Gb    |
| Client #2 |     Data Node + Node Manager + Flume + HBase     | t2.large  | 40Gb    |
| Client #3 |     Data Node + Node Manager + Flume + HBase     | t2.large  | 40Gb    |
| Client #4 |     Data Node + Node Manager + Flume + HBase     | t2.large  | 40Gb    |

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
  - if not available, please [follow this guide to add it to your Ambari](../Hue/hue_ambari.md)
- Slider

## Masters assignations list

Split the following services on the masters instances. We can review this assignment if needed in the future.

|            Services            |   Where   |
| :----------------------------: | :-------: |
|        NameNode (HDFS)         | Master #1 |
|        SNameNode (HDFS)        | Master #2 |
|   App Timeline Server (YARN)   | Master #3 |
|     ResourceManager (YARN)     | Master #3 |
|   History Server (MapReduce)   | Master #3 |
|  ZooKeeper Server (ZooKeeper)  | Master #1 |
|  ZooKeeper Server (ZooKeeper)  | Master #2 |
|  ZooKeeper Server (ZooKeeper)  | Master #3 |
|  Infra Solr Instance (Ambari)  | Master #2 |
|   Metrics Collector (Ambari)   | Master #2 |
|        Grafana (Ambari)        | Master #2 |
| Activity Analyzer (SmartSense) | Master #4 |
| Activity Explorer (SmartSense) | Master #4 |
| Spark2 History Server (Spark2) | Master #4 |
|  Spark History Server (Spark)  | Master #4 |
|    HST Server (SmartSense)     | Master #4 |
|        Hue Server (Hue)        | Master #8 |
|     Hive Metastore (Hive)      | Master #5 |
|     WebHCat Server (Hive)      | Master #5 |
|      HiverServer2 (Hive)       | Master #5 |
|      HBase Master (HBase)      | Master #5 |
|      Oozie Server (Oozie)      | Master #5 |
| Atlas Metadata Server (Atlas)  | Master #7 |
|      Kafka Boker (Kafka)       | Master #7 |
|      Knox Gateway (Knox)       | Master #6 |

## Slaves assignations list

I recommand to install on the four instances that we choose to be our data nodes (without the *✵* in the list), the following:

- DataNode
- NodeManager
- Client

Leave the rest as it is.

## Customize services list

Some services need require information from us, in order to work properly.

- [Hive](../Hive/ambari_install_customize.md)
- [Oozie](../Oozie/ambari_install_customize.md)
- [Knox](../Knox/ambari_install_customize.md)
- [SmartSense](../SmartSense/ambari_install_customize.md)
- [Ambari Metrics](../Metrics/ambari_install_customize.md)

The others services are good with the default parameters, but can also need some custom. Please edit this part if further custom of these services is needed.