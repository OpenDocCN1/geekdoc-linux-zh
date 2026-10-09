```
# Un-comment the following to provide a specific roving profile share
# the default is to use the user's home directory
;	[Profiles]
;			 path = /var/lib/samba/profiles
;			 browseable = no
;			 guest ok = yes

# A publicly accessible directory, but read only, except for people in
# the "staff" group
;	[public]
;		 comment = Public Stuff
;		 path = /home/samba
;		 public = yes
;		 writable = yes
;		 printable = no
```

![](bbox=[0.02, 0.33, 0.49, 0.36])

By default, the smb.conf file comprises three sections: global, homes, and printers. Each section consists of its own options specific to the share. The global section defines options such as the workgroup name, log size, and the security mode that are applicable to the server as a whole. It defines the default options that are common to all the other shares. The options given in the global section can be overridden by other sections. The homes section consists of options, such as browseable and writable, that define user access of files in home directories. The printers section consists of options, such as path and guest ok, that define the sharing of printers and their services.

```
[global]
#
# ---------------------- Network Related Options ----------------------
#
# workgroup = NT-Domain-Name or Workgroup-Name, eg: MID-EARTH
# server string is the equivalent of the NT Description field
#
# netbios name can be used to specify a server name not tied to the hostname

[homes]
		 comment = Home Directories
		 browseable = no
		 writable = yes
		 valid users = %S
;		 valid users = MYDOMAIN\%S

[printers]
		 comment = All Printers
		 path = /var/spool/samba
		 browseable = no
		 guest ok = no
		 writable = no
		 printable = yes
```

![](bbox=[0.02, 0.79, 0.52, 0.82])

Each section in the samba.conf file comprises its own options specific to the share. The syntax for defining an option is option = value. Some frequently used options are listed in the table.