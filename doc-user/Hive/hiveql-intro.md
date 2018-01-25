# Introduction for Hive HQL

## What is HQL

HQL is a SQL query-like language to query and manage large datasets. It's easy to learn if you're familiar with SQL.

## Uses and limitations of Hive

### Usages

- The Apache Hive distributed storage
- Hive provides tools to enable easy data extract/transform/load (ETL operations)
- It provides the structure on a variety of data formats
- By using Hive, we can access files stored in Hadoop Distributed File System

### Limitations 

- Hive supports overwriting or apprehending data, but not updates and deletes
- In Hive, sub queries are not supported
- Hive is not designed for Online transaction processing (OLTP ), it is only used for the Online Analytical Processing



## Components of Hive

### MetaStore

Hive stores the schema of the Hive tables in a Hive Metastore. It is used to hold all the information about the tables and partitions that are in the warehouse. 

### SerDe

Serializer, Deserializer gives instructions to hive on how to process a record.

## Links for useful information

Hive official home page :

https://hive.apache.org/

The Getting Started Guide on the Hive wiki :

https://cwiki.apache.org/confluence/display/Hive/GettingStarted

