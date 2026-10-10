the filesystem not covered by the standard.
The complete standard can be viewed at:

http://www.pathname.com/fhs/

# 10.1.1 Overview of the FSSTND

The directories and files noted here are a small subset of those specified by the FSSTND document. Check the latest FSSTND document for the most up to date and complete information.

# The /etc Directory

The /etc directory is reserved for configuration files that are local to your machine. No binaries are to put in /etc. Binaries that were in the past put in /etc should now go into /sbin or possibly /bin.

The X11 and skel directories should be subdirectories of /etc:

```
```text
/etc
 | \- X11
 +- skel
```
```

The X11 directory is for X11 configuration files such as XF86Config. The skel directory is for “skeleton” user files, which are files used to populate a home directory when a user is first created.

# The /lib Directory

The /lib directory should contain only those libraries that are need to execute the binaries in /bin and /sbin.

# The /sbin Directory

The /sbin directory is for executables used only by the root user, and only those executables needed to boot and mount /usr and perform system recovery operations. The FSSTND says: