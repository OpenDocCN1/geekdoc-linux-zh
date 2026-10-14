If a group of research users are working on a collaborative project, they may need to be segregated onto separate storage for the server to reduce their impact on other users. As part of the process, they should have their home directories placed there. Also, due to the nature of the research, only members of the group may have access to the mount point.

This result can be accomplished by specifying a new mount point in the root `/research`. A number of filesystems permit restricting access to the mounted partition to specific UID and GID. Mount does not support these features for ext3 or Reiser partitions. Access to specific individuals or groups therefore must be restricted a different way. The following steps can serve as a guide to creating a directory structure specific to the research group:

+   1. Create a group called `research` for the project.
+   2. Prepare the new partition using `fdisk` and `mkfs`.
+   3. Create a standard directory named `/research` for mounting the new resource.
+   4. Modify `/etc/fstab` to allow the partition to be mounted at boot time.
+   5. Execute a `mount -a` command to verify that the partition is mounted correctly.
+   6. Change the group membership of the mount point directory using `chgrp research /research`.
+   7. Change the access permissions on the mount point directory using `chmod 6770 /research`.
+   8. Create containers for the home directories of the users and one for the project data using `mkdir /research/home` and `mkdir /research/project`.
+   9. Adjust the permissions on these directories using `chmod 6770 /research/home` and `chmod 6770 /research/project`.

> **NOTE**
> 
> > In the preceding set of steps, the ownership of the root directory is left as root. This might seem counter-intuitive because you would probably like it to belong to a member of the group.
> >
> > Making a group member the owner of the directory generates another issue. If the selected individual leaves, his or her account will be deleted and the UID orphaned. Any new account accidentally given the same UID would automatically be granted access.