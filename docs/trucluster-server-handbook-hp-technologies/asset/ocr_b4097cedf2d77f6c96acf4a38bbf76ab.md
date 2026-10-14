very simple Tcl/Tk application that we wrote (see section 24.2.1), we will choose to have a default action script generated, and we will simply indicate the path to our application. Choosing to generate a default action script causes “sysman caa” to copy the template.scr script from the /var/cluster/caa/template directory and inserts the application name and resource name in the appropriate spots within the script.

```
grep -E "memberUP|hostname" /var/cluster/caa/script/memberUP.scr

SERVICE_NAME="memberUP"
PROBE_PROCS="/code/caa/xhostname"
START_APPCMD="/code/caa/xhostname"
```

Note that the action script name is the name resource name with a “.scr” extension. Also note that the script will be located in the /var/cluster/caa/script directory by default. We recommend that all action scripts remain in this default directory.

At this point you can choose to take the default profile attributes by clicking the **OK** button. Or you can choose to customize the profile attributes by clicking the **Options** button.

# 24.9.1.1 Customize Profile Attributes

The Options popup window includes the default values for the remaining attributes. The Options popup window for each resource type is shown in Figure 24-6.

![](bbox=[0.102, 0.53, 0.899, 0.899])