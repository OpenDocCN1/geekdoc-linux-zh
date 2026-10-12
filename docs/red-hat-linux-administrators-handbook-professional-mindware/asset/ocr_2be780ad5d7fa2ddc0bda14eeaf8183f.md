+   Verify that your /etc/services file has the following line:
+   
+   swat 901/tcp
+   
+   If the above line is not present, add this line and save the /etc/services file.

+   Verify that your /etc/xinetd.d/swat file has the following line:
+   
+   disable = no
+   
+   If the above line is missing, commented out, or set to yes, add or uncomment it such that disable is set to no. In such a case reconfigure xinetd daemon using the killall1 -USR1 xinetd command.

+   Next, run your favorite Web browser to access your Samba server. Enter the following URL:
+   
+   http://your-samba-server:901/

+   You will be asked to enter a username and password. Enter root as the username and the password. If you have entered an appropriate username/password pair, you will see the SWAT welcome screen.

+   Click on the available links to manage various aspects of Samba.

# Testing the /etc/samba/smb.conf configuration

Any time you change a Samba configuration file, run the testparm utility, which is bundled with the Samba package. When you run this nifty utility from the command line, it checks the syntax of the /etc/samba/smb.conf file and gives you useful warning and error messages. Because a misconfigured /etc/samba/smb.conf file can be a security hole, use this utility whenever you modify this file.

# Starting, stopping, and restarting the Samba service

After you make sure that your /etc/samba/smb.conf file is error-free, you are ready to start Samba. Two daemons come with the Samba package. The smbd daemon is the Samba server, and the nmbd daemon is the NetBIOS name server. To start the daemons, run the following command as root:

```
/etc/rc.d/init.d/smb start
```