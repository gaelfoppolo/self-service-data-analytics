# Hadoop

## Pre-Requisites

- 01-AWS completed
- OpenSSH installed or any SSH client

## Installation

In order to work, **each node** in the cluster **must have **Java and Hadoop installed. First Java:

```shell
sudo apt-get install default-jdk
```

Then Hadoop, download, uncompress and move it to `/usr/local/` folder.

```
wget http://apache.crihan.fr/dist/hadoop/common/hadoop-2.8.2/hadoop-2.8.2.tar.gz
sudo tar xzf hadoop-2.8.2.tar.gz 
sudo mv hadoop-2.8.2 /usr/local/hadoop
```

*Note*: why `/usr/local/`? The `/usr/local` hierarchy is for use when installing software locally. It needs to be safe from being overwritten when the system software is updated. It may be used for programs and data that are shareable among a group of hosts. This is perfect for Hadoop.					

##Global configuration

Now that Hadoop is installed, we need to configure the global environment variables. Perform the following on **each node**. Edit `~/.profile` and append the following at the end of it:

```
# Hadoop configuration
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
export PATH="PATH:JAVA_HOME/bin"
export HADOOP_HOME=/usr/local/hadoop
export PATH=PATH:HADOOP_HOME/bin
```

*Note:* change the JVM path according to yours.

Finally reload with: `. .profile `

## Hadoop cluster configuration

This section will cover the Hadoop cluster configuration. **Four main files** must be configured in order to specify to Hadoop various configuration. Here we are going to configure it to launch in a fully distributed mode (multi nodes cluster).

Each file is located in the `etc/hadoop` of the Hadoop install folder. For us the full path is : `/usr/local/hadoop/etc/hadoop`.

### **core-site.xml**

This file contains configuration settings for Hadoop Core (eg I/O) that are common to HDFS and MapReduce. It also informs Hadoop daemon where NameNode (the master) runs in the cluster. So each node must have this file completed.

Replace these two lines with the next block, and complete the master's private IP with your own.

```xml
<configuration>
</configuration>
```

```xml
<configuration>
    <property>
        <name>fs.default.name</name>
        <value>hdfs://<master's_private_IP>:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/home/ubuntu/hadooptmp</value>
        <description>A base for other temporary directories.</description>
    </property>
</configuration>
```

hdfs-site.xml

core-site.xml

yarn-site.xml

mapped-site.xml