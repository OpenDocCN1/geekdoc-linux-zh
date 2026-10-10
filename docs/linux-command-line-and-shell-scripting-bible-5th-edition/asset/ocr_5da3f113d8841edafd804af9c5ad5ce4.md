# Part I: The Linux Command Line

interactive login shell and as a shell script command processor. Of the standard shells, zsh most closely resembles ksh but includes many enhancements. Zsh has command-line editing, built-in spelling correction, programmable command completion, shell functions (with autoloading), a history mechanism, and a host of other features. $

> Note
> 
> The apt show command does not indicate that the package is installed on the system. It shows only detailed package information from the software repository.

One detail you cannot get with apt is a listing of all the files associated with a particular software package. To get this list, you need to use the dpkg command itself:

```
dpkg -L package_name
```

Here’s an example of using dpkg to list all the files installed as part of the acl package:

```
```
$ dpkg -L acl
/.
/usr
/usr/bin
/usr/bin/chacl
/usr/bin/getfacl
/usr/bin/setfacl
/usr/share
/usr/share/doc
/usr/share/doc/acl
/usr/share/doc/acl/copyright
/usr/share/man
/usr/share/man/man1
/usr/share/man/man1/chacl.1.gz
/usr/share/man/man1/getfacl.1.gz
/usr/share/man/man1/setfacl.1.gz
/usr/share/man/man5
/usr/share/man/man5/acl.5.gz
/usr/share/doc/acl/changelog.Debian.gz
$
```
```

You can also do the reverse—find what package a particular file belongs to:

```
dpkg --search absolute_file_name
```

Note that you need to use an absolute file reference for this to work:

```
```
$ dpkg --search /usr/bin/getfacl
acl: /usr/bin/getfacl
$
```
```

The output shows that the getfacl file was installed as part of the acl package.