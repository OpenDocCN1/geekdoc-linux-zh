```
```text
Company T64 UNIX V5.1A (Rev. 1885) (malari.gene.com) console
login: root
Password:

****************************************************************
The 'clu' cluster is currently in a rolled state and the software versions
that are available are different depending on which cluster member you
are on. Additional information about the exact state of the system
can be obtained using the /usr/bin/clu_upgrade command.
****************************************************************
```
```

17. At this point in the Upgrade Installation, we are just about done with this stage. The next step will be to verify that the Install Stage is complete and successful. See section 25.5.5.1.

# 25.5.4.2     Install Stage for a Patch Kit Installation

We’ve seen the individual steps required to perform the Install Stage for an Update Installation. Now let’s see what it takes to perform the Install Stage of a Patch Kit Installation:

+   1. Update the system firmware on the lead cluster member. Please review the Warning in section 25.5.1.3.
+   
+   2. We are now ready to install the Patch Kit. Again, the following commands must be executed on the lead member:
+   
+      - If installing the Patch Kit from multi-user mode:

```
```text
# cd /usr/patch_kit
# ./dpatch
```
```

← or where your Patch Kit is located

+   - If installing the Patch Kit from single-user mode:

```
```text
# shutdown -sb now
# bcheckrc
# reinit start
# cd /usr/patch_kit
# ./dpatch
```
```

← or where your Patch Kit is located

> **WARNING:**
> 
> While you have a choice of installing Patch Kits in either multi-user or single-user mode, we agree with HP in recommending that the Patch Kit installations should be performed in single-user mode. Doing so will reduce the risk of another Systems Administrator causing unintentional issues.