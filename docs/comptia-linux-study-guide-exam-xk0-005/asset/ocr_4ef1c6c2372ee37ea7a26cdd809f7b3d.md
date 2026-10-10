![](bbox=[0.14, 0.09, 0.33, 0.22])

After your Linux system has traversed the boot process, it enters final system initialization, where it needs to start various services. A service, or daemon, is a program that performs a particular duty. Several services were covered in Chapter 2, “Introduction to Services.”

The initialization daemon (init) determines which services are started and in what order. This daemon also allows you to stop and manage the various system services.

The SysV init (SysV) was based on the Unix System V initialization daemon. While it’s not used by many major Linux distributions anymore, you still may find it lurking around that older Linux server at your company.

The systemd initialization method is the new kid on the block. Started around 2010, it is now the most popular system service initialization and management mechanism. This daemon reduces initialization time by starting services in a parallel manner.

Beyond initialization, these daemons are also responsible for managing these services well past boot time. We’ll explore these concepts in this chapter.

# Looking at init

Before we start examining the various service management methods, it’s a good idea to take a look at the init program itself. Classically, service startups are handled by the init program. This program can be located in the /etc/ , the /bin/ , or the /sbin/ directory. Also, it typically has a process ID (PID) of 1.

The init program or systemd is the parent process for every service on a Linux system. If your system has the pstree program installed, you can see a diagram depicting this relationship by typing `pstree -p 1` at the command line.

This information will assist you in determining which system initialization method your current Linux distribution is using, systemd or SysV init. First find the init program’s location, using the which command. An example is shown in Listing 6.1.

```
```
# which init
/sbin/init
#  
```
```

Now that you know the init program’s location, using super user privileges, you can use the `readlink -f` command to see if the program is linked to another program, as shown in Listing 6.2.