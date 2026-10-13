# Testing the Samba Configuration

After you make your changes to the `smb.conf` file, you can then use the testparm program to see if the entries are correctly entered. testparm checks the syntax and validity of Samba entries. By default, testparm checks the `/etc/samba/smb.conf` file. If you are using a different file as your configuration file, you can specify it as an argument to testparm. You can also have testparm check to see if a particular host has access to the service set up by the configuration file.

With SWAT, the Status page will list your connections and shares. From the command line, you can use the `smbstatus` command to check on current Samba connections on your network.

To check the real-time operation of your Samba server, you can log into a user account on the Linux system running the Samba server and connect to the server.