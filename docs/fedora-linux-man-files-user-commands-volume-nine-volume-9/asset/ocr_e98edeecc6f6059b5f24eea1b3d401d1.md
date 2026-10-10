# DESCRIPTION

This tool is part of the **cifs-utils** suite.

setcifsacl is a userspace helper program for the Linux CIFS client file system. It is intended to alter an ACL of a security descriptor for a file system object. Whether a security descriptor to be set is applied or not is determined by the CIFS/SMB server.

This program uses a plugin to handle the mapping of user and group nas to SIDs. **/etc/cifs-utils/idmap-plugin** should be a symlink that points to the correct plugin to use.