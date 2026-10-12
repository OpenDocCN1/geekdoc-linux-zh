A sample etc/hosts.allow file, when edited to allow access to services, might look like this:

```
ALL: Centennial.edu

in.talkd: ALL

in.ntalkd: ALL

in.fingerd: ALL

in.ftpd: ALL
```

This configuration allows all connections from Centennial and Centennial.edu machines to use the services. It also allows the services talk, finger, and ftp to accept requests from all machines.

The tcpd program allows much more sophisticated access control, using a combination of the files /etc/hosts.allow and /etc/hosts.deny. The administrators of Centennial learned to use this technique to enable content management.

# Using an FTP Server to Download Files

An FTP server is configured and running after a standard Red Hat 6.0 installation. Users can use anonymous FTP to exchange files on Red Hat 6.0 system via any FTP client, including a Web browser. To demonstrate this capability, the administrators allowed several users to try this by entering their URL from any client that could access the Linux system over a network:

```
ftp://linux_system_name/
```

When using this command, users accessed the directory /home/ftp on the Red Hat 6.0 system. Any files that were placed in the directory /home/ftp/pub were accessible by default to anonymous users who logged in to the system using FTP.

FTP can also be used to access regular user accounts with a URL like this one:

```
ftp://username@linux_system_name/
```

The user gets prompted for a password before he or she can see the files on the Linux system. Several files located in the /etc directory define the configuration of the FTP server running on Red Hat 6.0. Although the default configuration is fairly secure, many