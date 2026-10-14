# 23.4.19.3 How Can I Determine Which Attribute Values are Registered For a Given Resource?

You can use the caa_stat command with "-p" switch to see the currently registered attribute values for a given resource. Note, this can be particularly useful in determining whether you remembered to update the registration of a resource after modifying its profile.

Note, that what is actually registered may be different from what is in your profile.

# Currently Registered (In Memory):

# In Profile:

```
# caa_stat -p nicUP
NAME=nicUP
TYPE=network
DESCRIPTION=nicUP
FAILURE INTERVAL=600
FAILURE THRESHOLD=2
SUBNET=192.168.0.0
```

```
# caa_profile -print nicUP
NAME=nicUP
TYPE=network
DESCRIPTION=nicUP
FAILURE INTERVAL=0
FAILURE THRESHOLD=0
SUBNET=192.168.0.0
```

Remember to update your registration when you modify your profile (see section 23.4.12).

# 23.4.19.4 How Can I See Which Resources are Running On a Particular Cluster Member?

The caa_stat command with the "-c hostname" switch can be used to retrieve resource status for a particular cluster member.

```
# caa_stat -t -c molari
Name          Type         Target   State    Host
----------------------------------------------------
clustercron   application  ONLINE   ONLINE   molari
memberUP      application  ONLINE   ONLINE   molari
nicUP         network      ONLINE   ONLINE   molari
```

For more information, see the caa_stat(1) reference page.

# 23.5 The Action Script

Every Application resource must have an action script. The action script starts and stops the application resource as well as optionally checking the status of the application resource.

The action script can be written in any language. The only requirement is that the script accept a "start", "stop", and (optionally) "check" arguments on the command line.

+   - myAppResource.scr start      - Starts myAppResource
+   - myAppResource.scr stop       - Stops myAppResource
+   - myAppResource.scr check      - Checks the status of myAppResource