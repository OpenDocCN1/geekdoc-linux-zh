```
#domainname sniglets.com
```

The ypinit command initializes a machine to become a master or slave server. To set up a master server, enter

```
#ypinit -m
```

You will be prompted for the names of additional slave servers. The slave servers do not have to be running NIS. Upon completion of the ypinit command, you should have a set of NIS maps for the sniglets.com domain under the /var/yp/sniglets.com directory.

The configuration files that build the NIS maps are currently located in the default location (/etc directory) on the master server. This allows any user in the NIS domain to be able to log in to the master server. This is not a good idea. The master server should be a secure workstation with only administrators having login privileges. Fixing this problem requires moving the NIS domain's password file (/etc/passwd) to a different location. For consistency and ease of use, copy all of the text configuration files to a new directory (/var/yp/files). This allows configuration of the NIS master server using local configuration files and maintains the NIS database in a separate location. Moving the configuration files to the /var/yp/files directory requires modification of the Makefile in the /var/yp directory. The following example contains a portion of /var/yp/Makefile for a Linux NIS master server. Skip down to the lines that begin with the following:

```
GROUP = $(YPWDDIR)/group
```

This is the portion of the Makefile that determines which text configuration files will be utilized to construct the NIS maps. All of the configuration files are preceded with either the YPPSRCDIR or YPWPDDIR variables. Since we have copied all of the configuration files to /var/yp/files, we need to change each one of these variables to point to the new location. To do this, we edit the Makefile and change the entries as depicted in Table 7.2.

| Table 7.2 Changing the Location of NIS Configuration Files |
| Current Line | Replacement Lines |
| YPSRCDIR = /etc | #YPSRCDIR = /etc
YPSRCDIR = /var/yp/files |
| YPPWDDIR = /etc | #YPPWDDIR = /var/yp/files |

> domainname used without an argument will display the domain name of the system. If an argument is used, the domain name is set to that. ypinit initializes a system to be an NIS server.