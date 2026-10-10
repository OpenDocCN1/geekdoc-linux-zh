wherever they are trying to go, no matter where they are at. If a Linux administrator is trying to go in and change something in the abc folder, they will just type in the command below:

```
$ cd /etc/var/abc
```

Linux is finicky about this whole change directory syntax. As we have mentioned before as well, capitalization matters in Linux. If you are trying to reach a folder whose name is written in all lowercase, and you type the folder in all capital letters, Linux will not be able to find it; it will say that the directory cannot be found.

All of this is important for you to understand. It can be extremely frustrating if you do not grasp it.

```
Welcome to the Ubuntu Server!
> Documentation: http://www.ubuntu.com/server/doc

System information as of Fri Aug 29 11:57:13 EDT 2010
System load: 0.0 Processes: 66
Usage of "/": 11.2% of 7.49GB Users logged in: 0
Memory usage: 14% IP address for lo: 127.0.0.1
Swap usage: 0% IP address for eth0: 10.0.2.15

Graph this data and manage this system at https://landscape.canonical.com/
@server:~$ cd /_
```

So, the first thing you want to do when navigating files and folders in Linux is make sure that you are in the root directory. To do this, you must type the command below:

```
$ cd /
```

That is cd, a space, and then a forward slash. This is automatically bring you to do the root directory if you are not already there. Now the next logical thing to do would be to see what folders are within the root folder itself. To do this, you must type the command below:

```
$ ls
```

The ls, or list command will list all the files and folders within a particular directory—root, in this case.