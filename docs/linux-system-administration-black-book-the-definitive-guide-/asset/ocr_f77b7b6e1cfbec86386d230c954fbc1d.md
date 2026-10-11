# Browsing In KFM

The KFM is simple to browse and works much like a Web browser. To move through the directory structure, do one of the following:

+   • Click on the item you want to open, whether it is a folder (directory) or an icon referring to a file.
+   *   Utilize the Location text box and type “file:path” for where you want to go. For example, “file:/usr/sbin”.
+   *   Click on the up arrow to move up in the directory tree.

> TIP: Click on the Home icon to return quickly to your home directory.

# Setting Up Disk Quotas

There are two different stages to setting up usage quotas. In the first stage, you configure the machine itself to look for the quotas. In the second stage, you assign the quotas.

# Preparing The Machine

To set up your machine to look for quota information, do the following:

+   1. Log in as root.
+   2. Use the **ed** command to go to the base directory for the partition you want to enforce quotas over. You must create quotas on a partition-by-partition basis; you cannot apply them only to particular directories.
+   3. Use the **touch** command to create the files “quota.user” and “quota.group”.
+   4. Open the file /etc/fstab to edit. If you are unused to working with this file or with your favorite editor, be sure to make a backup of it first.
+   5. Locate the line that defines the partition to which you want to add quotas.
+   6. Move the cursor to the mount options column (column 4).
+   7. If you’re using vi, press “i” to enter Insert mode.
+   8. Add the text “usrquota” to the end of the current options to add user quotas. If you want to assign quotas by group, add the text “grpquota”. You also can add both. An example of what the resulting file might look like is:

```
/dev/hda3   /tmp  ext2  defaults,usrquota,grpquota  1  3
```

> NOTE: If you are not sure if you want one of the options, go ahead and add it now.