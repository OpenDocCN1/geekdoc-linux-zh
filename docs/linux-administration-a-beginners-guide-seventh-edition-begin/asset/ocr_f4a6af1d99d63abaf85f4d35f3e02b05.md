# CHAPTER 18 Apache Web Server

# 483

NOTE In the event you decide to allow CGI or similar scripts on your server, pay strict attention to how they are written. Be sure it's not possible for input in over the network to make the CGI or similar script something it shouldn't. Although there are no hard statistics on this, some successful attacks on sites are possible because of improperly configured web servers and/or poorly written CGI or similar scripts.

# Installing the Apache HTTP Server

Most Linux distributions come with the binary package for the Apache HTTP server software in RPM or .deb format, so installing the software is usually as simple as using the package management tool on the system. This section walks through the process of obtaining and installing the program via RPM and Advanced Packaging Tool (APT). Mention is also made of installing the software from source code, if you choose to go that route. The actual configuration of the server covered in later sections applies to both classes of installation (from source or from a binary package).

On Fedora/RHEL/CentOS systems, you can obtain the Apache RPM in several ways. Here are some of:

+   Download the Apache RPM (for example, httpd*.rpm) for your operating system from your distribution's software repository. For Fedora, you can obtain a copy of the program from:

```
http://dl.fedoraaproject.org/pub/fedora/linux/releases/<VERSION>/Server/x86_64/os/Packages/h/
```

where <VERSION> refers to the specific version of Fedora that you are running (for example, 22, 23, or 40).

+   You can install from the media, from the /Packages/ directory on the media.

+   You can pull down and install the program directly from a repository using the dnf or yum application. This is perhaps the quickest method if you have a working connection to the Internet. And this is what we'll do here.

To use dnf to install the program, type the following:

```
root@fedora-server ~]# dnf install httpd
```

To confirm that the software is installed, type the following:

```
root@fedora-server ~]# rpm -q httpd
httpd-2.*
```

And that's it! You now have Apache installed on the Fedora server.