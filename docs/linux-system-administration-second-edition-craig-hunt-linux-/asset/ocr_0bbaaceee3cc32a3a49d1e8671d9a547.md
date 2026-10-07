Each line begins with a single IP address and is followed by one or more hostnames. (Typically, a full hostname is first, followed by one or more hostnames that lack the domain name, or synonyms.) If your network uses /etc/hosts, be sure that the file is present and that its contents are reasonable.

You may also want to check the /etc/host.conf file. This file tells Linux in what order to try various hostname resolution methods, among other things. It normally contains a line like the following:

```
order hosts,bind
```

This line specifies that Linux will use /etc/hosts followed by DNS (which sometimes goes by the moniker BIND, for Berkeley Internet Name Daemon). This line may contain additional entries, or entries in alternative orders. If it's missing either entry shown here, name resolution may be impaired on your local network or on the Internet as a whole, respectively.

# **Network Unreachable Message**

This message means that the local machine doesn't have a network route to the remote system. Verify the address you used. Use the netstat -r command to determine whether there is a route to the remote host's network.

# # Kernel Compilation

Compiling a kernel is not difficult if you know the process. Nevertheless, there are some common errors that appear on mailing lists with some frequency.

# **make menuconfig** Generates an Error about **ncurses.h**

You may type **make menuconfig** and get the following error:

```
make[1]: *** [lxdialog.o] Error 1
make[1]: Leaving directory `/usr/src/linux-2.2.16/scripts/lxdialog'
make: *** [menuconfig] Error 2
```

The problem is that you do not have the package installed that contains ncurses.h. This can be a little confusing because you may have the ncurses RPM installed and still get this error. On systems using the Red Hat Package Manager (RPM), you need to install the ncurses-devel RPM in order to use make menuconfig.

# **Signal 11 Error**

Sometimes when a user or a system administrator compiles a new kernel, gcc returns the following error:

```
gcc: internal compiler error 11
```

Signal 11 is a segmentation violation, which generally means that the program is trying to write into memory it doesn't own. The problem is usually caused by bad memory in your computer. If you immediately try to run the make command again and it goes a bit further, the problem is almost surely hardware. There is a great site that details signal 11 errors at http://www.bitwizard.nl/sig11/.