+   4. Verify that the /etc/mail/aliases file is up to date, but do not copy it to the DIR directory.
+   5. Remove comments and other unnecessary information from the copied source files. Verify that the file formats are correct.
+   6. Modify the /var/yp/Makefile to identify the selected DIR and PWDIR directories.

Use the following procedure to configure an NIS master server. As part of the procedure, the maps will be built automatically:

+   1. To be sure that the system is using the /etc files configuration for the name service switch, copy the /etc/nsswitch.files file to the /etc/nsswitch.conf file.
+   2. Add entries to /etc/hosts for each NIS slave server.
+   3. If necessary, use the **domainname**(1M) command to set the domain name.
+   4. Run the **ypinit**(1M) command to initialize the NIS master server and build the maps, as shown here.
+   5. Provide the information in response to the prompts from the **ypinit** command. This information includes a list of NIS slave servers and whether the **ypinit** command should exit if an error is encountered.
+   6. Enable NIS by copying the /etc/nsswitch.nis file to the /etc/nsswitch.conf file.

```
ypinit -m
```

To start the NIS master server, either reboot the system or run the **ypstart**(1M) command, as shown here:

```
/usr/lib/netsvc/yp/ypstart
```

# NIS Slave Server

You can use the following procedure to configure a system as an NIS slave server:

+   1. Configure the system as an NIS client. If necessary, use the **domainname** command to set the domain name.
+   2. Update the /etc/nsswitch.conf file to use NIS by copying the /etc/nsswitch.nis template file to it or by manually editing the appropriate configuration.