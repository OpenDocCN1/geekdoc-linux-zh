For printing to work properly, printing services must be set up correctly on your Red Hat computer. (See Chapter 12, "Printing Services," for more information.) A typical [printers] section will look like the following:

```
[printers]
comment = Red Hat Printers
browseable = no
printable = yes
path = /var/sp/samba
```

The /var/sp/samba is a spool path set for Samba printing.

# Testing Samba with the testparam command

Once you have created your /etc/smb.conf file, you can check it for correctness. This is done with the testparam command. This command will parse through your /etc/smb.conf file and check for any syntax errors. If none found, it's a good bet that your configuration will work correctly. It does not, however, guarantee that the services specified in the file will work. It is merely making that the service is correctly written.

As with all configuration files, if you are modifying an existing, working file, it is always prudent to copy the working file to a different location and modify it there. Then, you can check the file with the testparam utility. The syntax is as follows:

```
# testparam /path/to/smb.conf-back-up
Load smb config files from smb.conf-back-up
Processing section "[homes"
Processing section "[printers"
Loaded services file OK.
```

This output shows that the Samba configuration file is correct, and, as long as all the services are running correctly on your Red Hat computer, Samba should be working correctly. Now copy your old smb.conf file to a new location, put the new one in its place, and restart Samba with the command /etc/init.d/smb restart. Your new or modified Samba configuration should be in place.

# Starting the smbd Daemon

Now that your smb.conf file is correctly configured, you can start your Samba server daemon. This can be done with the /usr/sbin/smbd command, which (with no options) starts the Samba server with all the defaults. The most common option that you will change in this command is the location of the smb.conf file; change this option if you don't want to use the default location /etc/smb/smb.conf. The -s option allows you to change the new smb.conf file that Samba uses; this option is also useful for testing whether a new smb.conf file actually works. Another useful option is the -l option, which specifies the log file that Samba uses to store information.