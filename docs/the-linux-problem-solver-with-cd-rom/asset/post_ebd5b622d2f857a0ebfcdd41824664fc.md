
## Setting Up an NIS Client

1. Set the NIS domain name with the domainname command (here, the NIS domain name is *mydomain*).

```sh
# domainname mydomain
```

2. Make sure portmap is running and start up ypbind, which broadcasts over the network in an attempt to find an appropriate NIS server. If your subnet has an NIS server with your NIS domain name, the server should respond and ypbind on the client will bind to that server.

3. Check the server with the ypwhich command. If everything looks right, use ypcat to dump a map (for example, if there's a group map, use `ypcat group`).

If everything goes well, set up your files to get the information from ypbind like so:

**/etc/passwd**

The code

```
+::::::::
```

at the end of the passwd file allows all users in the passwd map to log in. If you want to limit access to only one user in the NIS passwd map, use

```
+user::::::
```

**netgroups**

To allow access to users in an NIS netgroup *ng*, add the line

```
+@ng::::::
```

The netgroup is particularly useful when you want to deny general user access to servers, which you would typically do with this type of passwd file:

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/sh
bin:x:2:2:bin:/bin:/bin/sh
...
... (other passwd entries)

+@sysadmins::::::
+::::::/usr/local/bin/noaccess
```

Here, sysadmins is a netgroup containing the user names of all systems administrators. The last line serves as a catchall so that the users are not unknown on the server. Failure to use proper user names will confuse or break many server daemons (Web servers, for instance).

## PROBLEM 20

Symptom: You can use ypcat netgroup, but your netgroup entries to /etc/passwd don’t actually seem to do anything.

Problem: Wrong /etc/nsswitch.conf.

Fix: If you’re going to use the netgroup at all, /etc/nsswitch.conf must have a line like this:

```
netgroup: ... nis
```

NOTE If you’re configuring Solaris NIS clients alongside your Linux clients, netgroup in /etc/nsswitch.conf is only valid with nis.

## PROBLEM 21

Symptom: Users can log in, even though you disallowed them with +@ng::::::/bin/noaccess in /etc/passwd.

Problem: Wrong /etc/nsswitch.conf.

Fix: /etc/nsswitch must have this line:

```
passwd: ... compat
```

On the other hand, the following will not work with the +/@ convention in /etc/passwd:

```
passwd: ... files nis
```

The fastest way to verify a user’s shell is with finger or with an ugly perl command such as

```
$ perl -e 'print join(" ",getpwnam(username)) . "\n"'
```

## Debugging with ypcat, ypmatch, and ypwhich

Part of debugging NIS clients is figuring out whether you’re actually getting the data you’re supposed to. The ypcat and ypmatch programs can help with this. ypcat simply dumps an NIS map to the standard output:

```
$ ypcat group
```

Use the -k option to ypcat to see the map’s keys in addition to its values.

> NIS is based on dbm files, so the output you get is in no particular order.

If you know exactly what you’re looking for and in which map to find it, use ypmatch:

```
$ ypmatch key map
```

This prints the value for key in map.
If you don’t know which NIS server your machine is bound to (if any), use ypwhich:

```
$ ypwhich
```

## NIS Servers

The server side of NIS consists of a collection of prototype files, dbm files generated from these files (these dbm files are the NIS maps when put on the network), some programs that perform the conversion, and the NIS server itself (ypserv). The NIS master server has all of these components, and they come with most Linux distributions. Slave servers only need ypserv, which looks at dbm files, usually located in /var/yp. Inside this directory, you’ll find a Makefile, your guide to how all the files fit together.

Before going through how to start up the NIS server (in the next subsection, Setting Up the NIS Master Server), let’s explore how a file gets into NIS map format with /var/yp/Makefile. We’ll look at passwd because it leads to the creation of more than one map.

Look in /var/yp/Makefile for the all: target (it’s about the 98th line in some distributions), and you’ll see passwd mentioned there. Ignore the passwd.adjunct for now. Now find the passwd: target (around line 123)—you’ll see that it actually references two more targets, passwd.byname and passwd.byuid, so go ahead and look for these (line 257). Skip past the MERGE_PASSWD stuff to this target:
