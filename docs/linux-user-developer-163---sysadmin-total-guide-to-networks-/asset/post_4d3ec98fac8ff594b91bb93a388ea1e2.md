
# Tutorial Hadoop

## Set up a Hadoop cluster

Break into Big Data by setting up a network of Hadoop nodes to process vast swaths of data

![](img/f4a034c4fbc20906a013558fa4e058a2_47_0.png)

**Ashish Sinha**
An author-developer, open source enthusiast, blogger and speaker. With over five years of experience in an MNC, Ashish enjoys exploring new open source technology and tools.

With the advent of new technology – a growing number of social networking sites, scientific research projects and new business models – data is growing rapidly. This data is minded to churn out the relevant information: data is studied to uncover hereditary diseases; data from shopping habits to weather station reports and new products are used for forecasting, and much. The emergence of an open source technology called Hadoop

Even the large database class is not recommended as they stand low on the price/performance graph. Typically, the choice of running HDFS and node manager would have the following specification:

- **Processor:** 4x8 octo-core 5 GHz CPUs
- **Memory:** 256GB ECC (Error Correcting Code) RAM (ECC)
- **Storage:** 12x4 x 1-TB SATA disks
- **Network:** Gigabit Ethernet with link aggregation

**Resources** Hadoop
bit.ly/20m12lh

Hadoop stores the data across several nodes in a cluster and the data is replicated in HDFS to ensure high availability and reduce fault tolerance. To store data that are terabytes or petabytes in size, we need to use commodity hardware which is scalable, distributed, fast and resilient to failure. In this tutorial, you will learn how to install and configure a Hadoop cluster using the Apache distribution on a low cost operating system.

The size of the cluster depends upon the data you want to store in. If you have 5 TB of data with replication factor of 3, then you will need 20 TB storage on HDFS. From the network perspective, a normal Hadoop cluster with 1 Gbps network per node, 10 Gb switch or router – a “rack” is a storage area with all the data nodes put together.

## Cluster specification and sizing

Hadoop works with commodity hardware, not “low-end”, as cheap machines have higher

## Java installation

The prerequisite to set up a Hadoop cluster is that you must have some basic knowledge of Java. Hadoop runs on both Unix and Windows and requires Java to be installed:

![](img/f4a034c4fbc20906a013558fa4e058a2_47_1.png)

**Right** The distribution layer represents your physical server racks, controlled by a core layer and serving requests to the access layer (ie, the client machines) in this case we will use a Linux machine.

The JDK for Linux from https://www.oracle.com/network/technology/java/javase/jdk7-downloads-1880260.html.
Now create the directory in root mode and install jdk, from the tar file using the commands below.

```
$ sudo su
$ mkdir /usr/lib/jvm
$ mv jdk7-u279-1586.tar.gz /usr/lib/jvm/
$ cd /usr/lib/jvm
$ sudo tar xzvf jdk7-u279-1586.tar.gz
```

Restart your terminal and then append the following lines to /etc/profile

```
JAVA_HOME = /usr/lib/jvm/jdk1.7_09
PATH = $JAVA_HOME/bin:$PATH
JRE_HOME = /usr/lib/jvm/jdk1.7_09
export JAVA_HOME=$JAVA_HOME
export JRE_HOME=$JRE_HOME
export PATH=$PATH
```

After appending the lines below run

```
sudo update-alternatives --install "/usr/bin/java" "/usr/lib/jvm/jdk1.7_09/bin/java" 1
sudo update-alternatives --install "/usr/bin/java" "/usr/lib/jvm/jdk1.7_09/bin/java" 2
sudo update-alternatives --set java /usr/lib/jvm/jdk1.7_09/bin/java
sudo update-alternatives --install "/usr/lib/jvm/jdk1.7_09/bin/java" 1
sudo update-alternatives --install "/usr/bin/java" "/usr/lib/jvm/jdk1.7_09/bin/java" 1
sudo update-alternatives --set java /usr/lib/jvm/jdk1.7_09/bin/java
```

Once this is done, restart the terminal and run command
java -version to check the Java installation. This step needs to be done in all of the machines.

## SSH configuration

After installing Java, we need to create a password-less key for the nodes of the cluster using SSH. Secure Shell (SSH) is a Unix-based communication interface to and access remote servers. Different users need password-less connections for this you need to generate one and share it across the cluster for every user. SSH in the client server, must use the open-ssh client in the master node. Since SSH uses port 22, it is open by default. master machine must install the open-ssh server by running y in the terminal to start the ssh services.

## Hadoop installation

The tarball for Hadoop can be downloaded from \apache.org/releases. For this article we are using Hadoop-2.0.0.tar.gz; use this file in the Hadoop installation.

## Storing data in HDFS

The data is copied from sources and kept in HDFS. Hadoop dfs -put is the command to put the file on HDFS. Hadoop does not have a ready directory, we have to create one manually using the command
hadoop dfs -put user/hadoop/output/

![](img/f4a034c4fbc20906a013558fa4e058a2_48_0.png)

it can be seen in the environment variables are stored in hadoop
![](img/f4a034c4fbc20906a013558fa4e058a2_48_1.png)

| File | Description |
| :--- | :--- |
| core-site.xml | Edit site-specific properties. |
| hadoop-env.sh | The required environment variable is JAVA_HOME. All others are optional! |

```
# core-site.xml
# The required environment variable is JAVA_HOME. All others are optional!
# When running a distributed configuration it is best to set JAVA_HOME in this file, as correctly defined in environment
# The Java implementation of use, in MB.
export JRE_HOME=/usr/lib/jvm/jdk1.7_09-jre
# The maximum amount of heap to use, in MB. Default is 1024.
export HADOOP_NODE_HEAP_SIZE="2000"
# Where log files are stored.
export HADOOP_LOG_DIR=/var/log/hadoop
# The Java implementation to use. Use native commands.
export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR="/etc/hadoop"
# Extra CLASPATH elements. Automatically insert capacity-scheduler
for f in ($HADOOP_HOME/capacity-scheduler/*.jar); do
if [ -z "$HADOOP_PATH" ]; then
export HADOOP_PATH=$HADOOP_PATH:$f
```

## Set up for production

directory by executing sudo tar -xvf Hadoop-2.2.0.tar.gz. The file contains the environment variables which are needed in hadoop-env.sh. The command JAVA_HOME=/usr/lib/jvm/java-8.0-openjdk needs to be edited to set the path to your Java installation. Also the value of HADOOP_HEAP_SIZE is edited to set the memory for each Hadoop daemon, which is by default 1GB, HADOOP_HOME is the path of logs if you configure separated directories; parameter ensures that logs are kept in one place. cluster is only one NameNode and multiple DataNodes, Since NameNode is a single point of failure, a SecondaryNameNode can exist on different machines, which store the image of the NameNode from time and act as a backup. The data in DataNodes is also replicated to ensure the high availability of data in any single DataNode is down the replication factor of three. All three copies are stored. To get a Hadoop up and running, the following properties need to be set:

- dfs.default.name - list of directories where the NameNode stores its partition data; contains comma-separated directories; default value is $HADOOP_HOME/hdfs
- dfs.data.dir - list of directories where the DataNodes store blocks; contains comma-separated directories; default value is $HADOOP_HOME/dfs
- dfs.checkpoint - list of directories where the NameNode stores checkpoints; contains comma-separated directories; default value is $HADOOP_HOME/hdfs/fsname

For a production cluster, the following settings are recommended:

## Configuration to Run Hadoop

To run three files need to be configured: core-site.xml, hdfs-site.xml, yarn-site.xml. The core-site.xml contains the configuration setting for core, hadoop sets the configuration to HDFS, YARN and Map Reduce. The IP address is configured with the IP of the node which acts as NameNode.

```
<configuration>
  <property>
    <name>dfs.default.name</name>
    <value>hdfs://10.0.1.113:9000</value>
  </property>
</configuration>
```

In hdfs-site.xml, the NameNode and DataNodes must be configured. The NameNode is the node in the cluster that stores the metadata of the data - like the number of blocks, on which the rack is stored and whereas the DataNodes are the machines that store the data blocks.

Moving on, next yarn-site.xml for YARN daemons, a resource manager, a web app server for YARN (Another Resource Negotiator) decouples MapReduce resource management and scheduling capabilities from the data processing component. Yarn provides its core services through two daemons called Resource Manager (per cluster), which manages the

For a production cluster, Hadoop's configuration settings are held in core-site.xml.

| File | Encoding |
| :--- | :--- |
| core-site.xml | UTF-8 |
| hadoop-env.sh | UTF-8 |

```
<?xml version="1.0" encoding="UTF-8"?>
<xml-stylesheet type="text/xml" href="configuration.xsd?>
<!--
Licensed under the Apache License, Version 2.0 (the "LICENSE");
You may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0 -->

Unless required by law or agreed in writing, distributed under the License is distributed on an "AS IS", WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations. Limitations under the License. Using accompanying permissions and --

--+ Put site properties overrides in this file. --
```
