While the easiest way to restore the original configuration is with the GUI SELinux management tool, you should also know how to use commands like the following, which disables a custom SELinux user type for user michael:

```
# semanage login -d michael
```

# Lab 8

Success in this lab can be measured first with the ls -Zd command. When applied to both the /ftp and the /var/ftp/pub directories, it should lead to the same list of SELinux roles, objects, types, and MLS options for each directory.

This lab also contains a solvable mystery. Why is it that the SELinux contexts of a newly created directory differ from those where the contexts have been restored with the restorecon command.

The basic reason is the difference between regular unconfined_u SELinux user types and the options listed in the file_contexts file in the /etc/selinux/targeted/contexts/files directory. You'll learn how to modify default file contexts in Chapter 11.

# Lab 9

Everyone will experiment with SELinux in different ways. So the results of this lab are up to you. The objective is to analyze a current relevant log file, and process it at the command line. Try to identify the problems associated with each alert. While you may not be able to address many SELinux issues, at least until the second half of this book, you should be able to identify the problems or at least the users and/or commands associated with each alert. If you don't have enough of a log, two related files are available in the Chapter4/ directory of the CD.