
## higher quality random number generation.

To add the service, issue the command

```
chkconfig --add name
```

where name is the name of the service. The chkconfig program creates the required symbolic links according to the comments in the init.d script.

## Deleting a Service

To delete a service, issue the command

```
chkconfig --del name
```

where name is the name of the service. The chkconfig program deletes the associated symbolic links.

## Associating a Service with Runlevels

To associate a service with one or more runlevels, issue the command

```
chkconfig name reset
```

where name is the name of the service. The chkconfig program creates the required symbolic links according to the comments in the init.d script. If you prefer, you can explicitly set a service to run or not at specified levels regardless of the contents of the associated init.d script. To specify levels at which the service should run, issue the command

```
chkconfig --level levels1 name on
```

where name is the name of the service and levels1 is a series of digits that specify the runlevels. For example, the command

```
chkconfig --level 35 lunch on
```

specifies that the lunch service will run at levels 3 and 5. To specify levels at which the service should not run, issue the command

```
chkconfig --level levels1 name off
```

where name is the name of the service and levels1 is a series of digits that specify the runlevels. For example, the command

```
chkconfig --level 24 lunch off
```

specifies that the lunch service will not run at levels 2 and 4.

Now, try your hand at Exercise 14.3, which requires you to use chkconfig.

## EXERCISE 14.3
### Associating Services with Runlevels

The RHCE exam is likely to require you to configure services to run at specified levels. Perform the following operations to verify your ability to do so:

- 1. Use chkconfig to determine what services run at runlevels.
- 2. Using a system that has Apache installed, configure the httpd service to run only at runlevel 5.
- 3. Use the init command to change the current runlevel so that you can verify that your change succeeded.

Look back to the chapter if you must, but be prepared to use chkconfig without help during the RHCE exam.

## The /etc/rc.d/rc.local Script

The /etc/rc.d/rc.local script is a special script run by symbolic links in the directories associated with runlevels 2, 3, and 5. Its start point is 99, which means it runs after all other runlevel scripts. By default, it creates

- /etc/issue file
- /etc/issue.net file

The /etc/issue file is listed when a user logs in by using a local console. By default, the file reports the release of Red Hat Linux and the kernel version:

Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.25-15 on an i686

The /etc/issue.net file is listed when a user logs in by using a remote console—for example, by initiating a Telnet session. By default, the file reports the release of Red Hat Linux and the kernel version:

Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.25-15 on an i686

It's considered good practice to change the contents of /etc/issue.net so that hackers gain less information about your system. You may also want to display a banner stating any restrictions on system use.

You can easily modify the /etc/rc/rc.local script to put a different message in /etc/issue.net or to perform other host-specific initialization. Since the script is executed, all other system services associated with the current runlevel should be operational when the script executes.
To learn more about the rc.local script, complete Exercise 14.4.

## EXERCISE 14.4
### The /etc/rc.d/rc.local Script

System administrators modify the rc.local script to customize system-up. To learn more about start-up, inspect the /etc/rc.d/rc.local script of a configured Red Hat Linux system to see what modifications, if any, the system administrator has made to the script.

## Summary

In this chapter, you learned about system initialization. The most important topics are covered:

- **System Initialization** When a system is booted, it runs the script /etc/rc.d/rc.sysinit, which initializes file systems and devices, and then the script /etc/rc.d/rc.rc, which initializes services.

- **The /etc/rc.d/rc.sysinit Script** The /etc/rc.d/rc.sysinit script performs over two dozen operations, ranging from setting networking to saving the boot log.

- **The /etc/rc.d/rc Script** The /etc/rc.d/rc script runs a series of scripts associated with the default runlevel. By symbolic links that reside in the directory named /etc/rc.d/rc?d, where ? is the default runlevel.

- **Runlevels** Red Hat Linux defines seven runlevels, numbered 0 to 6. System operation generally proceeds under runlevel 3 or 5. Other levels are useful for troubleshooting and repair.

- **Runlevel Scripts** The runlevel scripts reside in /etc/rc.d/init.d. They generally accept the arguments start, restart, status, init.

- **Symbolic Links to Runlevel** The symbolic link to a runlevel script has a name of the form XNService, where X has the value K or S, NN determines the order in which the script is run, and Service specifies the associated service. A K script is used to stop a service, and an S script is used to start a service.

- **Functions** The script /etc/rc.d/init.d/functions contains several useful functions. This file is sourced by other runlevel scripts.

- **Configuring Services** You can associate a service with a runlevel by using any of several utilities, including chkconfig, ksysys, ntsys, and tksys.

- **The /etc/rc.d/local Script** The /etc/rc.d/local script is used to perform locally specified initialization operations.

## Key Terms

Before going on to the next chapter, be sure you're familiar with the following terms:

- Priority
- Runlevel
- Runlevel script

## Additional Sources of Information

If you'd like further information about the topics presented in this chapter, you should consult The Official Red Hat Linux Reference Guide.

## Review Questions

- 1. Which of the following file systems is mounted first?
  - A. The non-root file systems, in read-only mode
  - B. The non-root file systems, in read-write mode
  - C. The root file system, in read-only mode
  - D. The root file system, in read-write mode
- 2. What script invokes the runlevel scripts?
  - A. /etc/rc.d/rc
  - B. /etc/rc.d/rc.local
  - C. /etc/rc.d/rc.serial
  - D. /etc/rc.d/rc.sysinit
- 3. Which of the following scripts would be executed first if all were part of the same directory?
  - A. K05alpha
  - B. K10beta
  - C. S01delta
  - D. S05gamma
- 4. To see the runlevels associated with the service grub, which command must be issued?
  - A. chkconfig
  - B. chkconfig grub
  - C. chkconfig --grub
  - D. chkconfig --list
- 5. Which of the following tools can be used only under X?
  - A. chkconfig
  - B. ksysys
  - C. ntsys
  - D. tksys
- 6. To change the information placed in /etc/issue.net, file should you modify?
  - A. /etc/rc.d/rc
  - B. /etc/rc.d/rc.local
  - C. /etc/rc.d/rc.serial
  - D. /etc/rc.d/rc.sysinit

# Answers to Review Questions

1. C. The system first mounts the root file system in read mode; later, it mounts all file systems in read-write mode.
2. A. The rc script invokes the scripts in the /etc/rc/d/r?.d directories.
3. A. The kill scripts are executed before start scripts; within a type, scripts are executed by priority.
4. D. The --list command causes chkconfig to list services and their associated runlevels.
5. B, D. The ksysv program requires X. The tsysv program uses the TK widget set and operates only under X.
6. B. The file rc.local builds the /etc/issue.net file.
