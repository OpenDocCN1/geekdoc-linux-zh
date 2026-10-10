# DESCRIPTION

This tool is part of the cifs-utils suite.

getcifacl is a userspace helper program for the Linux CIFS client file system. It is intended to display a security descriptor including ACL for a file system object.

This program uses a plugin to handle the mapping of SIDs to user and group names. /etc/cifs-utils/idmap-plugin should be a symlink that points to the correct plugin to use.

Fields of an ACE such as SID, type, flags, and mask are displayed separated by / . Numeric values of type, flags, and mask are displayed in hexadecimal format.