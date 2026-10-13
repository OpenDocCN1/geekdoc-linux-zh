always create a table where you define the machines and the processors that they are not allowed to use. Table 36.1 shows an example of such a table.

Table 36.1: Planning for CPU load balancing.

| Virtual machine | CPU0 | CPU1 | CPU2 | CPU3 |
|---|---|---|---|---|
| Main file and print server | true | true | false | false |
| E-mail server | true | true | false | false |
| Intranet server | false | false | true | true |
| Accounting server | false | false | true | true |
| IT test server | false | false | true | true |

Note: When you need to transfer any of these virtual machines to another server that has more or less processors, make sure that you reconfigure the CPU scheduling for the new server.

# 37.2 Changing Port Numbers for VMware Virtual Machine Console

By default, your GSX Server listens on port 902 for connections from the client console application. If for any reason you need to change this to another port, you can do that by changing the parameters in the configuration files. After changing the port number, you can access the GSX Server by adding the new port number to the host name or IP address with a colon. For example: 192.168.1.10:9020.

# Windows

On the VMware GSX Server, add this line to your configuration file or modify it when it already exists:

```
authd.port = <portNumber>
```

This configuration file is called config.ini and it is located at the following location:

```
C:\Documents and Settings\All Users\Application Data\VMware\VMware GSX Server
```

After modifying this setting, you need to restart the VMware Authorization Service. You can do that from the Services Control Center, in Administrative Tools. Running virtual machines are not affected.

# Linux

On a Linux host, the files you need to modify will depend on whether you are using xinetd or inetd. If you are using inetd, the port number will be specified in file /etc/inetd.conf. If you are using xinted, modify the already existing port number parameter in the file in /etc/xinetd.d/vmware-authd:

```
port = 902
```