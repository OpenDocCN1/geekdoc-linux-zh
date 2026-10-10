# On the amanda server

To offer these services to the network in Fedora, you need to configure the `xinetd` daemon to listen for those services.

This enables Amanda to accept requests from the client system and to start the backup process without any user intervention. Next, enable the service for the `xinetd` daemon. To do this, edit the configuration file for Amanda in the `/etc/xinetd.d` directory and change the disable setting from `yes` to `no`. Then, on the `server_args` line, add `amindexd` and `amidxtaped` after `amdump` to the `-auth=bsd` option.

You need to tell the `xinetd` daemon to reload the `/etc/xinetd.d` files before this change takes effect. You can do this by typing the following as root user:

```
# /etc/init.d/xinetd reload
```

# On each amanda client

Next you need to configure the `.amandahosts` file in the `/var/lib/amanda` directory on each computer (client) that the amanda server will back up from. This file should contain the fully qualified host and domain name of any backup servers that will connect to this client. When you begin, only your localhost is defined in this file as your backup server. To add another computer as a backup server, type the following (replacing *amanda1host* with the name of the backup server, while you are logged in as the amanda user):

```
$ echo amanda1host >> /var/lib/amanda/.amandahosts
```

Note that you *may* need to include the Amanda user name:

```
$ echo amanda1host amandabackup >> /var/lib/amanda/.amandahosts
```

You also need to make sure that the amanda client daemon is configured to run on the client. You do this by enabling the amanda service by typing the following (as root user):

```
# chkconfig amanda on
```

This enables the amanda client to communicate with the amanda server. You need to tell the `xinetd` daemon to reload the `/etc/xinetd.d` files before this change takes place. Do this by typing the following as root user:

```
# /etc/init.d/xinetd reload
```

# Performing an Amada backup

Now that everything is configured, you are ready to perform an Amada backup. Before running the actual backup, you should run `amcheck` to check your drive and configuration. While logged in as root, change to the amandabackup user and then type the following commands: