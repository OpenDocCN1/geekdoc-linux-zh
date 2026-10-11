
# 03 Munin master web server configuration

There are a number of situations where you'd like to run munin-node on hosts not directly available to the Munin server.

![](img/1f330653f83dcf0397f7d224ce8bbc16_42_0.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_42_1.png)

The file you will be modifying is apache.conf, Munin's Apache configuration file. This file is sym-linked to /etc/apache2/conf-available/munin.conf, which, in turn, is sym-linked to /etc/apache2/conf-enabled/munin.conf. Open the file to allow editing:

```bash
sudo nano apache.conf
```

At the very top of the file, modify the first line to /var/www/munin, the same as the htmldir path you specified in munin.conf. Next, look for the Directory section, and change the directory to /var/www/munin. Also comment out the first four lines and then add two new directives so that it reads:

```apache
<Directory /var/www/munin>
  Order allow,deny
  #Allow from localhost
  #Allow from 127.0.0.0/8 ::1
  #Options None

  Require all granted
  Options FollowSymlinks SymLinksIfOwnerMatch
</Directory>
```

You need to change the last and second-to-last Location sections in a similar manner to finish the configuration. Finally, restart the Apache and munin-node services. You should then be able to access Munin at http://localhost/munin.

# 04 Adding nodes

To configure Munin nodes, you'll need to edit the /etc/munin/munin.conf file. The first step is to allow access to the master, so it can query the node. A Munin node listens on all interfaces by default, but because of restrictive access lists, you need to add your master's IP address for the monitoring to work. The cidr_allow, cidr_deny, allow and deny statements can be used to list the master's IP address. With cidr_allow you can use the following syntax:

```conf
cidr_allow 127.0.0/8
```

Uncomment all these folder paths by removing the preceding # sign. Also, be sure to change the htmldir from /var/cache/munin/www to the actual web directory as per the web server configuration. We have used the path, /var/www/munin.

Next, look for the first host tree. It defines how to access and monitor the host machine. It should read:

```conf
[localhost.localhost]
address 127.0.0.1
use_node_name yes
```

Change the name of that tree to one that uniquely identifies the server. This is the name that will be displayed in the Munin web interface. Then, you'll need to add all the nodes you'd like to monitor in one of these formats. For example, add a node's IPv4 address using this format:

```conf
[node.example.com]
address 192.0.2.4
```

If you have DNS configured, you can also use the FQDN of the node instead of its IP address.

```conf
[node2.example.com]
address node2.example.com
```

Munin also supports IPv6, so you can add a node's IPv6 address in the below format.

```conf
[node3.example.com]
address 2001:db8:de:caf:bad
```

## Munin-node for Windows

Munin-node for Windows (munin-node-win32) is a Windows client for the Munin monitoring system. It's written in C++ with most plugins built into the executable. This differs from the standard munin-node client, which only uses external plugins written as scripts and Perl scripts. The configuration file munin-node.ini uses the standard INI file format.

# 05 Monitor hosts that aren't directly reachable

There are a number of situations where you'd like to run a Munin node on hosts not directly available to the Munin server. For example, consider a scenario where a UNIX server sits between the Munin server and one or more Munin nodes. The server in between reaches both the Munin server and the Munin node, but the Munin server cannot reach the Munin node or vice versa. There are various approaches to handle such scenarios: we'll look at SSH tunneling. With SSH tunneling, only one SSH connection is required, even if you need to reach several hosts on the other side. The Munin server can listen to different ports on the localhost interface and track the nodes. To enable tracking via SSH tunneling you need to add a node like this:

![](img/1f330653f83dcf0397f7d224ce8bbc16_43_0.png)

```text
[ssh-node]
address 127.0.0.1
port 5050
```

Then establish an SSH connection using the following:

```text
$ ssh -L 5050:localhost:4949 -f -N -i keyfile user@ssh-node
```

This will establish a tunnel between TCP ports 5050 on the calling machine to 4949 on the called machine. It will also send SSH in the background after possibly asking for a passphrase.

Now allow users by regular expression matching against the client IP address:

```text
cidr_allow 192.0.2.1/32

allow '^127.*'
allow '^192.0.2.1$'
```

The next step in configuring the Munin node is to decide which plugins to use. Once you have decided, just add the plugin file to the directory /etc/munin/plugins. The Munin node runs all plugins present in that directory.

Note that Munin has a plug-and-play architecture with no restrictions on how and where a node can be added to the network. So, whenever you need to add a new node to your existing network (that is being monitored by Munin), you can simply install the Munin node using the command mentioned earlier and allow access to the Munin master (using the configuration explained earlier). This will ensure the new node is being monitored by Munin.

![](img/1f330653f83dcf0397f7d224ce8bbc16_43_1.png)

![](img/1f330653f83dcf0397f7d224ce8bbc16_43_2.png)

# 06 Munin plugins

A Munin plugin is a simple executable invoked in a command line environment, whose role is to gather a set of facts on a host and present them in a format Munin can use. A plugin is usually called without any arguments. In this circumstance, the plugin returns the data in a key value format. For example, the load1 plugin, which comes as standard with Munin, will output the current system load:

```text
$ munin-run load
load.value 0.03
```

The default directory for plugins is /usr/share/munin/plugins/. You can activate a plugin by creating a symbolic link in the /etc/munin/plugins/ (for a package installation of Munin) and restarting the Munin node.

The Munin installation procedure uses the utility munin-node-configure to check which plugins are suitable for your node and create the links automatically. It is called every time a system configuration changes (services, hardware, etc) on the node and it will adjust the collection of plugins accordingly.

# 07 Munin plugin invocation

By default, about a dozen sets of plugins are installed and active. In its most common form, a plugin is a small Perl program or shell script.

The plugins are run by munin-node, and they are invoked when successfully contacted by the munin master. When this happens the munin-node runs each plugin twice – once with the argument config to get graph configuration, and once again with no argument to get graph data. This is how they're handled in a plugin.

When a plugin is invoked with the config argument it is expected to output configuration information for the graph it supports. This output will consist of a number of attributes divided into two sets -- global attributes and another set of data source-specific attributes. You can check out the details at this link: [http://munin.readthedocs.io/en/latest/reference/plugin.html](http://munin.readthedocs.io/en/latest/reference/plugin.html).

However, when the node receives a fetch command for a plugin the plugin is invoked without any arguments on the command line and is expected to emit one or more field, value attribute values, one for each thing the plugin observes as defined by the config output. The plotting of graphs may be disabled by the config output.

```shell
case $1 in
config)
cat <<'EOM'
graph_title Load average
graph_label Load
label.load Load
EOM
exit 0;;
esac

printf "load.value "
cut -d' ' -f1 /proc/loadavg
```

## Munin alarms

Mumina is a generic interface for receiving warnings and errors. If a Munin plugin discovers that a data source is breaching its defined limits, Mumini is able to alert the administrator either through more command-line invocations or through using a monitoring system like Nagios or Kanga. Note that if the receiving system can accept only a limited number of messages at a time, you can use the directives contact, contact_max_messages.

# 08 Sample Munin plugin

Let's create a simple Munin plugin. We'll take the example of the Load Average plugin and write it in shell script. In this plugin we want to be able to track a node's overall average load. There is a Linux file that has the info: /proc/loadavg. So, let us first read the file and format the output:

```bash
$ cut -d' ' -f1 /proc/loadavg
0.09
```

Also, Munin wants the value in a more structured form, so let's structure it further:

```bash
# printf "load.value "; cut -d' ' -f1 /proc/loadavg
load.value 0.06
```

Here the load is called the field or field name, the value is the attribute, and the number is the value. The next step is to make sure the plugin accommodates the mandatory requirement of responding with graph-related details when called with the config argument. Minimal output should look like this:

```text
graph_title Load average
graph_label Load
load.label load
```

This is to make sure that when munin-master gets data from the plugin, it knows how to plot the data in a graph. Here is the final plugin in one file.

```bash
#!/bin/sh
case $1 in
config)
cat <<'EOM'
graph_title Load average
graph_label Load
load.label load
EOM
exit 0;;
esac

printf "load.value "
cut -d' ' -f1 /proc/loadavg
```

> "The plugins are run by munin-node, and invoked when contacted by the munin master."

![](img/1f330653f83dcf0397f7d224ce8bbc16_44_0.png)

# 09 Munin buddyinfo plugin

Linux manages virtual memory on a page granularly. There are some operations, however, which require physically contiguous pages to be allocated by the kernel.

Such allocations may possibly fail if the memory gets fragmented, even when there are enough pages free, but they are not contiguous.

```text
/proc/buddyinfo
```

The /proc/buddyinfo file helps to visualise free memory fragments on your Linux machine. The Munin buddyinfo plugin can track this info on all the nodes of your network and help you monitor it from the master. This plugin monitors the amount of contiguous areas, called higher order pages. The order means the exponent of two of the size of the area, so order 2 means 2^2 = 4 pages.

![](img/1f330653f83dcf0397f7d224ce8bbc16_44_1.png)

# 10 Munin proc plugin

The Munin proc plugin is used to monitor various aspects of named processes. You can configure it by supplying a pipe-delimited list of parameters through environment variables. env_procname defines the processname as seen inside the parentheses of the second column in /proc/PID/stat. If you don't get the data you expect, you can check if the value is what you expect here. This is used for the first filter. Then args/user-filter is applied on top of this filter. Note that <PID> is the process ID of the process that you are interested in. Process names including non-alphanumeric characters (like space, dash, etc) are Special Names. Also, note that if the process name (in env_procname) contains any characters other than [a-zA-Z_], they will be internally replaced by underscores.
