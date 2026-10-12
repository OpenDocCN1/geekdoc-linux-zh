You can also upgrade your system software by using the rpm command's -F or “freshen” option, which fetches a designated package from a remote FTP or HTTP server. For example, to upgrade the fetchmail-conf package, use rpm like this:

```
```
# rpm -Fv ftp://ftp.tux.org/linux/redhat/updates/9/en/os/i386/
initscripts-7.14-1.i386.rpm
Retrieving ftp://ftp.tux.org/linux/redhat/updates/9/en/os/i386/
initscripts-7.14-1.i386.rpm
Preparing packages for installation...
initscripts-7.14-1
```
```

Use the -e option, along with the name of a software package, to remove or erase software from your system with rpm. For example, to remove the unace archiving package, use the rpm command like this:

```
```
# rpm -e unace
```
```

Note that if the operation succeeds, no messages will be displayed on your system. You can quickly search for the names of installed packages by piping the output of rpm -qa through the grep and sort commands (refer to Chapter 5, “First Steps with Fedora,” for additional information on grep and sort); here’s how to do that search:

```
```
# rpm -qa | grep mail | sort
fetchmail-6.2.5-7.fc4.1
mailcap-2.1.19-1
mailx-8.1.1-44
procmail-3.22-16
sendmail-8.13.4-2
system-switch-mail-0.5.25-4
system-switch-mail-gnome-0.5.25-4
```
```

This example returns a sorted list of all packages with names containing the word mail.

> **NOTE**
> 
> Another essential feature of the rpm command is its --rebuilddb option. If your system's RPM database becomes corrupted, this is your first (and perhaps only) option for restoring software management services. We hope that you never have to use this option; help ensure that by always backing up your data!

# ## Package Organization with RPM

Software packages on your Fedora system are organized into various groups, as you see later in this chapter. Using a group organization helps Fedora keep software organized by category and provides for hierarchical listings of software when using graphical RPM clients. You never have to manipulate these groups, but understanding the concept of package organization can help you gain familiarity with the way Fedora works.