```
root# testparm
```

Alternatively, where you are operating from a master configuration file called smb.conf.master, the following sequence of commands might prove more appropriate:

```
root#  cd /etc/samba
root#  testparm -s smb.conf.master > smb.conf
root#  testparm
```

Note any error messages that might be produced. Proceed only if error-free output has been obtained. An example of typical output that should be generated from the above configuration file is shown here:

```
Load smb config files from /etc/samba/smb.conf
Processing section "[data]"
Loaded services file OK.
Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions
[Press enter]

# Global parameters
[global]
       workgroup = MIDEARTH
       netbios name = HOBBIT
       security = share

[data]
       comment = Data
       path = /export
       read_only = Yes
       guest_only = Yes
```

+   6. Start Samba using the method applicable to your operating system platform. The method that should be used is platform dependent. Refer to Section 40.5 for further information regarding the starting of Samba.

+   7. Configure your MS Windows client for workgroup *MIDEARTH*, set the machine name to *ROBBINS*, reboot, wait a few (2 - 5) minutes, then open Windows Explorer and visit the Network Neighbourhood. The machine *HOBBIT* should be visible. When you click this machine icon, it should open up to reveal the *data* share. After you click the share, it should open up to reveal the files previously placed in the */export* directory.

The information above (following # Global parameters) provides the complete contents of the /etc/samba/smb.conf file.