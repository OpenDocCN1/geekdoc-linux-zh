# 7.1.2 File Servers

File servers under Windows work differently from the way they work in a Unix environment. In particular, remote file access is built into the operating system, without requiring mounted file systems like NFS, for example. Windows files may be accessed remotely via their Universal Naming Convention (UNC) or by mapping the share to a local drive via Windows Explorer. For example, if you have a file server with the name of “fileserver1” and it has a shared folder called “tools,” you can access this folder remotely from the command line by UNC as follows:

```
c:\ dir \\fileserver1\tools
```

or you can map it to a drive letter from the command line as follows:

```
c:\ net use Z: \\fileserver\tools
```

After issuing this command the local Z: will appear as if it were a local file system. Storage on several file servers can be logically aggregated into a single logical volume via Microsoft’s distributed file system (DFS). DFS allows multiple physical disk volumes to be accessed through a single shared volume. All cluster nodes can map this share as the same drive letter to provide a consistent interface across all cluster resources. Of course, this configuration does raise a potential problem: normally all mapped drives are disconnected when you log off the machine console. To work around this, you have two options. The first is to lock the screen and leave the console logged in with the drive mapped. This is sufficient if you have a secure machine room, but it is not the most elegant solution. The second option is to use a Windows service to map the drive, which will continue running even when you are not logged in at the console. The following simple Perl script uses a special module called Win32::Daemon (from Roth Consulting) that allows the script to act as a Windows service. You can download this module from www.roth.net/perl/.

```
#!perl
use Win32::Daemon;

%ModelHash =
    ( 
     name    => 'Model',
     display => 'Model Perl Service',
     path    => 'c:\perl\bin\perl.exe',

```