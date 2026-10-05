# Centralizing account management

not able to read immediately. You can defeat sendmail's default behavior by adding a fake shell named SENDMAIL/ANY/SHELL/ to the /etc/shells file.

# 7.9 MANAGING USERS WITH SYSTEM-SPECIFIC TOOLS

HP-UX and AIX provide a comprehensive system administration tool that how to manage users, at least in a rudimentary fashion. In AIX's SMIT, the System Management Interface Tool, and in HP-UX it is now called smh, the System Management Interface Homepage. (It was called sam, the System Administration Manager, in earlier HP-UX releases.) Each of these tools screens for adding and managing users, either with a windows-based GUI or with a terminal interface based on curses library. If you are a new sysadmin or an old hand on a new and different operating system, these are a reasonable place to start for many of the common sysadmin tasks.

AIX' sm has a handy feature; it shows the command and arguments that it is executing. It also logs all interactions and a script file of the commands it executed on your behalf. This can be a good learning tool as you become familiar with AIX's quirks. HP-UX's smh has nice single-character shortcuts for its curses interface. They are shown on each menu page so you can quickly get to the command you need.

# 7.10 REDUCING RISK WITH PAM

Pluggable Authentication Modules (PAM), are covered in the Security chapter starting on page 908. They central the management of the system's authentication facilities through standard library routines to programs like login, sudo, password, and do not have to supply their own tricky authentication code. PAM reduces the inherent risk in writing secure software, allows administrators to set site-wide security policies, and defines an easy way to add new authentication methods to the system.

Adding and removing users does not involve fiddling the PAM configuration under PAM's rules and constraints. In addition, many of the PAM configuration parameters are similar to those used by useradd and usermod. If you change a parameter as described in this chapter and useradd doesnt seem to be paying attention to it, check to see if the system's PAM configuration is overriding your new value.

# 7.11 CENTRALIZING ACCOUNT MANAGEMENT

Some of centralized account management is essential for medium-to-large enterprises of all types, they be corporate, academic, or governmental. Users need the convenience and security of a single login name, UID, and password across the site. Administrators need a centralized system that allows changes (such as account revocations) to be instantly propagated everywhere.

![](bbox=[0.943, 0.387, 0.99, 0.562])