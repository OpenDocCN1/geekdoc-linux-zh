# ## Using createrepo

createrepo is a program designed to quickly and efficiently draw the relevant informa-  tion from a collection of rpm files to make the metadata yum requires to successfully install  or update your currently installed package base.

The command is simply

```
`createrepo /yourtargetdirectoryhere`
```

So, if we were to use the example in the previous section, the syntax would look some-  thing like this:

```
`$ createrepo /home/andrew/repo`
```

This would give you the following output:

```
`88/88 - alsa-lib-1.0.6-5.i386.rpm`   
`Saving Primary metadata`   
`Saving file lists metadata`   
`Saving other metadata`
```

This shows that 88 RPMs were cataloged and that the relevant metadata was saved. The  program automatically uses the given directory, so you do not have to worry about  making several copies of directories.

After this is done, you are ready to include your new repository into the `/etc/yum.conf`  file or into its own file under `/etc/yum.repo.d`. Let's take a look at a typical configuration  file for use with yum:

```
`$ cat /etc/yum.repos.d/local.repo`   
`[local]`   
`name=Fedora Core $releasever - $basearch - Updates`   
`baseurl=http://192.168.2.5/repo`   
`enabled=1`   
`gpgcheck=0`
```

This file is fairly easy to read. Line one is the name of the repository that is passed to yum.  The name must be enclosed in square brackets for it to be picked up; in this case, it is  simply local. Line two gives us the display name for yum to show while it is busy  working; for this repository, it uses `Fedora Core $releasever - $basearch - Updates`,  which prints the release version (in this case 4) and the base architecture (i386). Next  comes the base URL, or the primary download point. This is used for yum to scan and  download the metadata it needs. The fourth line shows whether this repository is  enabled: `enabled=0` means it is disabled, and `enabled=1` means it is enabled and able to be  used. The final line determines whether the RPMs are checked using a GnuPG key. You  are advised to obtain the relevant GnuPG key from the original repository to ensure that