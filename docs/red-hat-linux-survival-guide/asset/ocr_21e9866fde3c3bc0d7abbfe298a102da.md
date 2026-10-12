# Chapter 14

# Configuring FTP Services

# IN THIS CHAPTER

+   - Setting up FTP service
+   - Setting up an anonymous FTP site
+   - Configuring a guest FTP account
+   - Setting up virtual FTP sites
+   - Becoming an efficient FTP user

Red Hat Linux ships with the wuarchive-ftpd, which is the default FTP server. More affectionately known as wu-ftpd, it is an FTP server daemon developed at Washington University. The most popular FTP server on the Internet, wu-ftpd is used on thousands of FTP sites all around the world.

If you choose to install FTP service during the Red Hat Linux installation, the wu-ftpd server is installed by default. However, if you are not sure whether or not you have already installed the wu-ftpd server, you can just query the RPM database of installed packages as follows:

```
rpm -qa | grep wu-ftpd
```

The rpm -qa command lists all the installed RPM packages, and the piped grep wu command matches the wu-ftpd pattern in the package names that are output by the rpm command, thus enabling you to see if any package has the wu-ftpd string pattern in its name. For example, the preceding command shows wu-ftpd-2.6.1-16 on my Red Hat Linux machine. The version number on your system will vary, as a new version of wu-ftpd is likely to be shipped with later versions of Red Hat Linux.