If you need to stop the NIS server at any time, you can do so with this command:

```
[root@arrakis /root]# /etc/init.d/ypserv stop
```

# ## Editing the Makefile

You may be familiar with using the **make** command to compile programs. The **make** tool doesn’t do the compilation, however—it simply keeps track of what files need to be compiled and then invokes the necessary program to perform the compilation. The file that actually contains the instructions for **make** is called a *Makefile*.

The **make** tool is efficient because the programs it invokes are arbitrary. You can substitute your preferred compiler in place of the one that comes with your Linux distribution, for example. When **make** sees that a file’s date and time have been modified, it takes that to mean that the file’s contents have been modified. If the file has been modified, that tells **make** that the file needs to be recompiled.

Putting this concept to work on NIS is very straightforward. In this case, there’s a series of straight text files that need to be converted into database format. We want a tool that will reconvert any files that have been changed—you can see how **make** fits the bill!

Changing over to the /var/yp directory, we see a file called **Makefile** (yes, all one word). This file lists the files that get shared via NIS, as well as some additional parameters for how they get shared and how much of each one gets shared. Open up **Makefile** with your favorite editor, and you can see all the configurable options. Let’s step through the makefile options that apply to us.

# ## Designating Slave Servers: NOPUSH

If you plan to have NIS slave servers, you’ll need to tell the master NIS server to push the resulting maps to the slave servers. Change the NOPUSH variable to false if you want slave servers.

> **NOTE**
> 
> If you don’t need slave servers now but think you will need them later, you can change this option when you do add the servers.

```
# If we have only one server, we don’t have to push the maps to the
# slave servers (NOPUSH=true). If you have slave servers, change this
# to “NOPUSH=false” and put all hostnames of your slave servers in
# the file /var/yp/ypservers.
NOPUSH=true
```

Remember to list the host names of your slave servers in the /var/yp/ypservers file; and for each host name you list there, be sure to list a corresponding entry in the /etc/hosts file.