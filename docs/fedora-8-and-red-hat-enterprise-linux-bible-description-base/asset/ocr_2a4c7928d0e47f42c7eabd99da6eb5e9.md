> **NOTE:** Another great command for copying files over the network is the `rsync` command. I often use `rsync` to do backups over the network. See Chapter 13 for descriptions on using `rsync` to do backups.

If there is a file you want to download from an FTP site or Web server (HTTP), and you know exactly where the file is, `wget` is a good way to download. The `wget` command is very useful if you want to copy a whole site, recursively, from one computer to another (for example, containing user home directories). When downloading from FTP sites, `wget` can let you just download as the anonymous user or add your own user name and password to the command line.

# **Downloading a single file**

Here is an example of using `wget` to get a file from a Web server:

```
```
$ wget http://dag.wieers.com/packages/pan/pan-0.14.2.91-2.1.fc3.rf.i386.rpm
--09:34:11--	http://dag.wieers.com/packages/pan/pan-0.14.2.91-2.1.fc3.rf.i386.rpm
			-> 'pan-0.14.2.91-2.1.fc3.rf.i386.rpm'
Resolving dag.wieers.com... 212.204.244.42
Connecting to dag.wieers.com[212.204.244.42]:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: http://apt.sw.be/packages/pan/pan-0.14.2.91-2.1.fc3.rf.i386.rpm [following]
--09:34:17--	http://apt.sw.be/packages/pan/pan-0.14.2.91-2.1.fc3.rf.i386.rpm
			-> 'pan-0.14.2.91-2.1.fc3.rf.i386.rpm'
Resolving apt.sw.be... 193.1.219.82
Connecting to apt.sw.be[193.1.219.82]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1,224,357 [application/x-redhat-package-manager]

100%[======================================================================] 1,224,357	53.23K/s	ETA 00:00

09:34:41 (52.08 KB/s) - 'pan-0.14.2.91-2.1.fc3.rf.i386.rpm' saved [1,224,357/1,224,357]
```
```

By the first part of the URL (`http://`), `wget` knows you are copying a file from an HTTP server to the current directory (`.`) on the local host. After resolving the address (`dag.wieers.com`), `wget` connects to the site and transfers the file. As the file downloads, `wget` shows the progress of the download, and then exits.

# **Downloading a file with user name and password**

If you are doing an FTP file copy and need to log in as a user other than anonymous, you can add that information to the command line or to a `.netrc` file in your home directory (type `man netrc` to see the format of that file). Here is an example of adding the password to the command line:

```
```
$ wget ftp://joe:m%76chevy@ftp.handsonhistory.com/memol.doc
```
```