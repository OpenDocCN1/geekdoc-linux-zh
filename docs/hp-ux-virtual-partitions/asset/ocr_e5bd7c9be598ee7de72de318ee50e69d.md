# ServiceControl Manager (SCM) Overview



```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

Please enter the file path where mxsetup will store the backup data (default path: /var/opt/mx/data/scm.backup) : 

```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

=====================================================================
ServiceControl Manager configuration has 'B' Tasks and it may take a while to do the configuration.

Please wait while mxsetup configures the ServiceControl Manager...
=====================================================================
1: Creating Agent Depots..
2: Naming the ServiceControl Managed Cluster as 'servicecluster'........................ OK
3: Configuring the ServiceControl daemons............ OK
4: Starting the ServiceControl daemons.............. OK
5: Installing the AgentConfig....................... OK
6: Initializing ServiceControl...................... OK
7: Adding Tools ..................................... OK
8: Backing up the Repository........................ OK
The ServiceControl Manager was successfully configured
Please see /var/opt/mx/logs/scmgr-setup.log for details.

To start the ServiceControl Manager:
- set DISPLAY environment variable
- and enter '/opt/mx/bin/scmgr'
#