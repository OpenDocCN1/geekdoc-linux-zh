This chapter details the commands used to manage files and directories, including copying, moving, renaming, and deleting files or directories. The commands used to change file ownership and set permissions are also covered.

# AT A GLANCE

| How Do I | See This Entry | Example |
| --- | --- | --- |
| Make sure my files cannot be altered by other users? | chmod | chmod o-w |
| Assign ownership of a file to a different user group? | chgrp | chgrp authors proposal.doc. |
| Set the ownership of a file to numeric permission mode 755? | chmod | chmod 755 welcome.html |
| Modify a file so that it executes with the set user ID (SUID) bit set? | chmod | chmod u+s ballistic |
| Set the permissions of all the files in the working directory so that the user has read and write privileges, group owners have read privileges, and others have no privileges? | chown | chmod u=rw,g=r |
| Change the owner of a file? | chown | chown suzanne proposal.doc |
| Change the ownership of all the files in an entire directory? | chown | chown -R suzanne * |