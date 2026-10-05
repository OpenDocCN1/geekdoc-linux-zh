in this case we will use a Linux machine.
The JDK for Linux from https://www.oracle.com/network/technology/java/javase/jdk7-downloads-1880260.html.
Now create the directory in root mode and install jdk, from the
tar file using the commands below.

```
$ sudo su
$ mkdir /usr/lib/jvm
$ mv jdk7-u279-1586.tar.gz /usr/lib/jvm/
$ cd /usr/lib/jvm
$ sudo tar xzvf jdk7-u279-1586.tar.gz
```

Restart your terminal and then append the following lines
to /etc/profile

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
```

sudo update-alternatives --install "/usr/bin/java" "/usr/lib/jvm/jdk1.7_09/bin/java" 1
sudo update-alternatives --set java /usr/lib/jvm/jdk1.7_09/bin/java

Once this is done, restart the terminal and run command
java -version to check the Java installation. This step needs
to be done in all of the machines.

# SSH configuration

After installing Java, we need to create a password-less
key for the nodes of the cluster using SSH.
Secure Shell (SSH) is a Unix-based communication interface
to and access remote servers. Different users need
password-less connections for this you need to generate one\and share it across the cluster for every user. SSH in the
client server, must use the open-ssh client in the
master node. Since SSH uses port 22, it is open by default.
master machine must install the open-ssh server by running
y in the terminal to start the ssh services.

# Hadoop installation

The tarball for Hadoop can be downloaded from\apache.org/releases. For this article we are using
Hadoop-2.0.0.tar.gz; use this file in the Hadoop installation

# Storing data in HDFS

The data is copied from
sources and kept in
HDFS. Hadoop dfs -put
system... is the command to put
the file on HDFS.
Hadoop does not have an
ready example directory,
we have to create one manually using
"Output directory."\ Make a directory using the
command
hadoop dfs -put
user/hadoop/data/output/

![](bbox=[0.763, 0.365, 0.813, 0.463])

it can be seen in the
sified file.

Left all
environment
variables are stored
in hadoop-env

![](bbox=[0.763, 0.815, 0.813, 0.913])

| core-site.xml |

| Edit View Save Options Undo Documents Help

```
# hadoop-site.xml variables
# The required environment variable is JAVA HOME. All others are
# optional! When running a distributed configuration it is best to
# set JAVA_HOME in this file, as it is correctly defined in
# environment
# The Java implementation of heap to use, in MB.
export JRE_HOME=/usr/lib/jvm/jdk1.7_09-openjdk-1.7.0/jre
# The maximum amount of heap to use, in MB. Default is 1024.
# export HADOOP_HAMENODE_INIT_HEAP_SIZE="2000"
# Where log files are stored. HADOOP_HOME_DIR/logs by default.
export HADOOP_LOG_DIR=/var/log/hadoop
# The Java implementation to use. Use is required to secure native commands.
# export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR="/etc/hadoop"
# Extra Java CLASPATH elements. Automatically insert capacity-scheduler.
for f in ($HADOOP_HOME/capacity-scheduler/*.jar); do
if [ -z "$HADOOP_PATH" ]; then
export HADOOP_PATH=$HADOOP_PATH:$f
```

www.linuxuker.com 49