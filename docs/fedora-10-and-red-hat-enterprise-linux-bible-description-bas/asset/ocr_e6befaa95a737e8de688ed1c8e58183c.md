# Chapter 13: Backing Up and Restoring Files 567

# On the amanda server

To offer these services to the network in Fedora or RHEL, you need to configure the xinetd daemon to listen for those services. You do this by enabling the amandaix and amidxtape services by typing the following (as the root user):

```
# chkconfig amidxtape on
# chkconfig amandaix on
```

This enables amanda to accept requests from the client system and to start the backup process without any user intervention. You need to tell the xinetd daemon to reload the /etc/xinetd.d file before this change takes effect. You can do this by typing the following as root user:

```
# /init.d/xinetd reload
```

# On each amanda client

Next you need to configure the .amandahosts file in /var/lib/amanda directory on each computer (client) that the amanda server will back up from. This file should contain the fully qualified host and name of any backup servers that will connect to this client. When you begin, your localhost is defined in this file as your backup server. To add another computer as a backup server, type the following (replacing amanda with the name of the backup server, which you are logged in as the amanda user):

```
$ echo amanda >> /var/lib/amanda/.amandahosts
```

You also need to make sure that the amanda daemon is configured to run on the client. You do this by enabling the amanda service by typing the following (as the root user):

```
# chkconfig amanda on
```

This enables the amanda client to communicate with the amanda server. You need to tell the xinetd daemon to reload the /etc/xinetd.d files before this change takes effect. Do this by typing the following:

```
# /init.d/xinetd reload
```

# Performing an Amanda backup

Now that everything is configured, you are ready to perform an Amanda backup. Before running the actual backup, run amcheck to check your directory and configuration. While logged in as root, type the following commands:

```
# /usr/sbin/amcheck DailySet1
# /usr/sbin/amdump normal
```

This runs the amanda command and tells it to read the configuration files it finds in the /etc/amanda/normal directory created earlier. It works its way down the list of systems and partitions in the disklist file, backing up each partition in the order it occurs. The results of the amdump are written to the /var/lib/amanda/normal directory. Read