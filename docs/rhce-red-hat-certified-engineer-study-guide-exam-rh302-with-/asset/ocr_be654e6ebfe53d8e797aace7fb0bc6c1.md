# 500 Chapter 21 · Installing and Configuring Primary Network Services

Web site, www.apache-ssl.org, or from ftp.zedz.net. Alternatively, you can use the Apache SSL module, mod_ssl or purchase a commercial version of Apache that provides SSL support, such as that sold by Red Hat.

# Installation

To install the standard version of Apache, move to the directory containing the RPM packages and issue the following command:

```
rpm -Uvh apache-[^d]*.rpm
```

If you need to be able Apache modules, you should also install the apache-devel package:

```
rpm -Uvh apache-devel-*.rpm
```

The [d] in the command to install the apache package prevents simulation installation of the apache-devel package.

![](bbox=[0.136, 0.461, 0.199, 0.513])

If you prefer to access Apache documentation from your local hard drive rather than the Web, you can install the apache-manual package, which places important Apache documents in /home/httpd/html/manua1/.

# Basic Configuration

The configuration files for Apache reside in /etc/httpd/conf. They are:

+   - access.conf
- httpd.conf
- srm.conf

At one time, each file contains directives of a particular sort. More recent versions of Apache have relaxed restrictions on file content, so the presence of three files can be viewed as a mere historical artifact.

The current version of Red Hat Linux places all of the configuration information in the file httpd.conf; the other two files contain comment lines, which have a hash mask (#) as the first non-blank character. The httpd.conf has three main sections, which are marked off by comments:

+   - Section 1, the global environment

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com