# ## Configuring an FTP Greeting Banner

Once you've installed the `vsftpd` FTP server, there are all sorts of ways you can configure it to behave as you want. Here's a simple example. We can change the default greeting message that the FTP server issues to clients on connection, simply by changing the value of the `ftpd_banner` directive in `/etc/vsftpd/vsftpd.conf`. For example, try changing it to this:

```
"# You may fully customize the login banner string:
ftpd_banner=Welcome to the Wrox Press FTP service."
```

Then restart the `vsftpd` service, so that the change takes effect. Now use your FTP client to log in to the FTP server, and you'll be greeted with this new message:

```
$ ftp 192.168.0.99
Connected to 192.168.0.99 (192.168.0.99).
220 Welcome to the Wrox Press FTP service.
. . .
```

For more information about the `vsftpd` FTP server, and all the configuration possibilities, refer to the man pages by typing `man vsftpd` and `man vsftpd.conf`. You can find also more information about the `vsftpd` FTP server at [http://vsftpd.beasts.org/](http://vsftpd.beasts.org/).

# ## Setting up a Print Server

If you want to share a single printer (or group of printers) among a number of users, then what you need is a **print server**. The print server manages the print requests and puts them into a queue for processing. It can manage:

+   - Sharing of printers between many users
+   - Authentication, so that only permitted users can print to a given printer
+   - Print queues
+   - Configuration of many printers in a single location

In this section we will examine how to configure our Linux machine as a print server for managing print jobs.

# ## Print Servers on Redhat Linux 9

Red Hat Linux 9 provides two different print server software packages: **cups** and **LPRng**. The **LPRng** package relates the old line printer daemon, and while popular for many years is now being superseded by the more recent **Common UNIX Printing System** (CUPS). CUPS is a printing service for Unix-based platforms, capable of managing printer jobs and queues and supporting network printer browsing.