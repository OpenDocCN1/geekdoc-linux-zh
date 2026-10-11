not always available. Therefore, the URL may also contain a username and password preceding the hostname:

```
ftp://smith:mypass@ftp.gnomovision.com/pub/rpms/foo bar-1.0-1.i386.rpm
```

However, entering a password where it can be seen by anyone looking at your screen is a bad idea. So try this format:

```
ftp://smith@ftp.gnomovision.com/pub/rpms/foo bar-1.0-1.i386.rpm
```

RPM will prompt you for your password, and you'll be in business:

```
# rpm -i ftp://smith@ftp.gnomovision.com/pub/rpms/apmd-2.4-1.i386.rpm

Password for smith@ftp.gnomovision.com: mypass (not echoed)
```

After you enter a valid password, RPM installs the package.

On some systems, the FTP daemon doesn't run on the standard port 21. Normally this is done for the sake of enhanced security. Fortunately, there is a way to specify a nonstandard port in a URL:

```
ftp://ftp.gnomovision.com:1024/pub/rpms/foo bar-1.0-1.i386.rpm
```

This URL will direct the FTP request to port 1024. The --ftport option is another way to specify the port. This option is discussed later in the chapter, in section 2.4.15.

# ### 2.2.2. A Warning Message You Might Never See

Depending on circumstances, the following message might be rare or very common. While performing an ordinary install, RPM prints a warning message:

```
# rpm -i cdp-0.33-100.i386.rpm

warning: /etc/cdp-config saved as /etc/cdp-config.rpmorig
```

What does it mean? It has to do with RPM's handling of config files. In the previous example, RPM found a file (/etc/cdp-config) that didn't belong to any RPM-installed package. Because the cdp-0.33-100 package contains a file of the same name that is to be installed in the same directory, there is a problem.

RPM solves this the best way it can. It performs two steps:

+   1. It renames the original file to cdp-config.rpmorig.
+   2. It installs the new cdp-config file that came with the package.

Continuing our example, if we look in /etc, we see that this is exactly what has happened:

```
# ls -al /etc/cdp*

-rw-r-- 1 root root 119 Jun 23 16:00 /etc/cdp-config

-rw-r-- 1 root root 56 Jun 14 21:44 /etc/cdp-config.rpmorig
```