# Chapter 5: Accessing and Running Applications 191

Besides downloading and installing new software packages, yum can also be used to check for available updates and list various kinds of information about available packages.

# Configuring yum (/etc/yum.conf)

The /etc/yum.conf file already comes preconfigured to include options that affect how you download and use RPM packages with yum. All necessary, basic repository lists are contained in files of the /etc/yum.repo directory. Here is what the yum.conf file contains:

```
[main]
installroot=/mnt/simage
cachedir=/var/cache/yum
keepcache=0
debuglevel=0
logfile=/tmp/yum.log
metadata_expire=1800
exactarch=1
obobsoletes=True
pluginpath=/usr/lib/yum-plugins,/tmp/updates/yum-plugins
pluginconfpath=/etc/yum/pluginconf.d,/tmp/updates/pluginconf.d
gpgcheck=1
plugins=1
```

+   # PUT REPOS HERE OR IN SEPARATE repo files
# /etc/yum.repo.d

The cachedir(/var/cache/yum) is where the RPM files are downloaded to yum when you ask to install or upgrade packages. The keepcache=0 option causes all downloaded packages and headers to be erased after they are installed. If you select to save the RPM files (some people do if they want to share packages with multiple machines, without multiple downloads), you need to set keepcache=1 and make sure the directory has enough space to handle it. During a testing cycle, I ended up with about 1GB of RPMs in my /var/cache/yum file system (of course, they can be deleted after they are installed).

> NOTE: You can clean out a lot of the data cached by yum with the command clean all.

Messages related to yum processing are sent to /tmp/yum.log by default, using a debug level of 2 (0 to 10 is legal, with 2 producing minimal success or failure messages). The exactarch set to 1 indicates that you must match the name and release architecture exactly for a package.

The obsolete option yum determine obsolete packages during updates. The gpgcheck indicates whether or not a check of the package's GPG key is done (1 indicates the check is done). With plugins turned on (set to 1), available extensions to yum are