# **Listing 11-1 The default /etc/samba/smb.conf file**

```
/etc/samba/smb.conf

# This is the main Samba configuration file.
# You should read the smb.conf(5) manual page in
# order to understand the options listed
# here. Samba has a huge number of configurable
# options (perhaps too
# many!) most of which are not shown in this example
#
# Any line which starts with a ; (semi-colon) or a
# (hash) is a comment and is ignored. In this example
# we will use a for commentary and a;
# for parts of the config file that you
# may wish to enable
#
# NOTE: Whenever you modify this file you should
# run the command "testparm" to check that you
# have not many any basic syntactic errors.

# =================Global Settings ======================
[global]

# workgroup = NT-Domain-Name or Workgroup-Name
workgroup = MYGROUP

# server string is the equivalent of the NT
# Description field
server string = Samba Server

# This option is important for security.
# It allows you to restrict connections to machines
# which are on your local network. The following
# example restricts access to two C class networks and
# the "loopback" interface. For more examples of
# the syntax see
```