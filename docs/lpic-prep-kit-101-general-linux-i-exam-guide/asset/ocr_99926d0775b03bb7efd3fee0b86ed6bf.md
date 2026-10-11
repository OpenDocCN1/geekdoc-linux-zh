You should never directly edit the /etc/shadow or /etc/gshadow files. When you need to change a user's or group's password, use a utility such as useradd, passwd, usermod, or gpasswd to make changes to it.

To begin using shadow passwords, use the pwconv command, which takes no arguments. When you run this command, it creates a /etc/shadow file from your /etc/passwd file. You always can convert back by using the pwunconv command. Using the pwunconv command will update your /etc/passwd file and then delete the /etc/shadow file.

To use shadow passwords for groups, use the grpconv command. This will create a /etc/gshadow file and change all the passwords in the /etc/group file to x. To revert to saving group passwords in the /etc/group file, run the command grpunconv.

If you must edit the /etc/passwd and /etc/group files by hand, you can update your shadow passwords by rerunning the appropriate commands—pwconv for /etc/passwd and grpconv for /etc/group. A better way is to first use pwunconv and grpunconv to stop using shadow passwords, make your changes, and then convert back to using shadow passwords.

![](bbox=[0.16, 0.46, 0.22, 0.53])

> **Key Concept**
> Shadow passwords increase the security of your system. Use pwconv to implement shadow passwords for your users and grpconv to use shadow passwords for your groups.

# User Startup Files

The look and function of your shell results from the use of environment variables. These parameters are saved in various configuration files located either in /etc or /home/\<username\>. The default environment variables for bash when started as an interactive login shell are located in the /etc/profile file. The following is an example of a profile file:

```
```
# /etc/profile

# System wide environment and startup programs
# Functions and aliases go in /etc/bashrc

PATH="$PATH:/usr/X11R6/bin"
PATH="$PATH:/usr/local/bin/blender"
PS1="[\u@\h \W]\$ "
BLENDERDIR=/usr/local/bin/blender
export  BLENDERDIR
```
```