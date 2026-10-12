Here are some examples:

+   Stop the database, all instances, and all services.
+       ```
+       srvctl stop database -d seed
+       ```

+   Stop named instances.
+       ```
+       srvctl stop instance -d seed -i seed1,seed2
+       ```

+   Stop the service.
+       ```
+       srvctl stop service -d seed -s CRM
+       ```

+   Stop the service at the named instances.
+       ```
+       srvctl stop service -d seed -s CRM -i seed2
+       ```

+   Stop node applications.
+       ```
+       srvctl stop nodeapps -n rac1
+       ```

![](bbox=[0.04, 0.46, 0.13, 0.54])

> **NOTE**
> 
> *Instances and services also stop when the nodeapps are stopped.*

Next, I’ll show how to modify the CRS. Here is the syntax:

```
```
srvctl modify database -d <name> [-n <db_name] [-o <ohome>] [-m <domain>]
                     [-p <spfile>] [-r {PRIMARY | PHYSICAL_STANDBY | LOGICAL_STANDBY}]
                     [-S <start_options>]
srvctl modify instance -d <database-name> -i <instance-name> -n <node-name>
srvctl modify instance -d <name> -i <inst_name> (-S <asm_inst_name> | -r)
srvctl modify service -d <database-name> -S <service_name> -i <instance-name>
                     -t <instance-name> [-f]
srvctl modify service -d <database-name> -S <service_name> -i <instance-name>
                     -r [-f]
srvctl modify nodeapps -n <node-name> [-A <address-description> ] [-x]
```
```

Here are the options for the preceding commands:

+   -i <instance-name> -t <instance-name> (The instance name [-i] is replaced by the instance name [-t].)

+   -i <instance-name> -r (The named instance is modified to be a preferred instance.)

+   -A address-list (For a VIP application, at node level.)

+   -S <asm_inst_name> (To add or remove an ASM dependency.)