The following is an example of a shadow password file:

```
root:$1$Vgk34Aeldk3XyMu2Pot5jdi9dQrmOW:11376:0:99999:7:::
jason:$1$nm2dkL9Z828BEtINXUPMKWxXrafHA:11406:0:99999:7:::
angie:$1$1639jnrB$mr9ZOeE3hZQzuN7hKvoTI:11406:0:99999:7:::
```

The pwconv tool is used to convert normal passwords to shadow passwords. Since some information needed is not in /etc/passwd, pwconv uses the PASS_MIN_DAYS, PASS_MAX_DAYS, and PASS_WARN_AGE from /etc/login.defs to populate these needed fields. To undo the conversion you can use pwunconv.

The /etc/group file can also be converted to use shadow passwords using grpconv. This tool creates a gshadow file that stores the encrypted passwords. To undo the change use the grpunconv tool.

> Shadow passwords are also covered in Chapter 10.

# Removing unused services

By default, most Linux distributions come with far more services enabled than the user needs. Distribution makers enable servers to reduce support calls from users that expect a service to be there that isn't. The problem with this practice is that most users end up running services they do not need, and they don't know it. When a security problem is found with a service, the users do not know they need to update their system, which leads to a lot of vulnerable systems.

The lesson here is to install and run only services that you need. This begins during installation. It’s definitely easier to choose one of the automated install paths that most Linux distributions offer, but you get much more granular control when doing a customized setup and picking and choosing the installed packages. The time spent here saves you from having to remove and disable services later.

The first step is removing unneeded services in the scripts directory where some services are started. These are /etc/rc.d/rcrunlevel>.d for Red Hat and /etc/rcrunlevel>.d for Debian. Remove any unneeded scripts for the runlevel that your system normally operates in.

The next place to look is the inetd.conf file. It is easy to overlook this and end up with a number of services running that you did not anticipate. Any unneeded entries should be commented out. If you do not require any services listed in inetd.conf, there is no reason to even run inetd. Remove its script from your runlevel directory.

The final step is to do a complete process list, such as ps aux, and look at all running daemons and processes. Make sure you know what each process does and if it is required. It is common for a normal workstation to need almost no server