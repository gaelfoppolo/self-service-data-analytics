# Install Hue

How to install Hue standalone.

## Pre-Requisites

- To know how to launch & config EC2 instance
- OpenSSH installed or any SSH client

## What will we do?

First we are going to create the instance we need. Then we will launch the install and config the components.

We will need **an EC2 instance**:

- running **Ubuntu Server 16.04 LTS**
- type **t2.medium**
- with **15Gb** of storage

When created and ready, let's begin!

## Install

SSH into it and run the following command, to install the dependencies:

```shell
sudo apt-get install git ant gcc g++ libffi-dev libkrb5-dev libmysqlclient-dev libsasl2-dev libsasl2-modules-gssapi-mit libsqlite3-dev libssl-dev libxml2-dev libxslt-dev make maven libldap2-dev python-dev python-setuptools libgmp3-dev
```

todo: need these ones ?

libtidy-0.99-0

python-simplejson

build-essential

In order to work, Hue **must have **Java installed.

```shell
sudo apt-get install default-jdk
# add it to the env
echo "JAVA_HOME=\"/usr/lib/jvm/java-8-openjdk-amd64/jre\"" | sudo tee -a /etc/environment
```

Download Hue on the server or on your machine and transfer it. Then unzip it and install:

```
scp -i hadoopec2cluster.pem ../bin/hue-4.1.0.tgz ubuntu@<public DNS>:~
tar -xvzf hue-4.1.0.tgz
sudo make install
```

By default, Hue installs to `/usr/local/hue` in your gateway node’s local filesystem.

As installed, the Hue installation folders and file ownership will be set to the `root` user.

Let’s fix that so Hue can run correctly without root user permissions:

```
sudo chown -R ubuntu:ubuntu /usr/local/hue
```

## Configuration

//todo

## Launch!

```
/usr/local/hue/build/env/bin/supervisor
```

We can access Hue through the browser, to `http://<public DNS of your Hue server>:8888`.

