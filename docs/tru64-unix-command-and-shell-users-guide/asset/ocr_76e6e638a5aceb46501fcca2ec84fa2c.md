By using the System V habitat scripts to alter the PATH environment variable, the System V habitat path can be changed without an administrator updating each user's .profile or .login and .cshrc files. The administrator simply updates the /etc/svid2path and /etc/svid3path files to enable global definitions.

To further illustrate how the System V habitat script sets a PATH, look at the following .profile file which specifies the System V habitat script for SVID 2:

```
stty erase DEL kill ^U intr ^C quit ^X echo
TERM=vt100
PATH=$HOME/bin:/usr/lib:/bin
MAIL=/usr/mail/$LOGNAME
EDITOR=vi
export MAIL PATH TERM EDITOR
if [ -f /etc/svid2_profile ]
then
    . /etc/svid2_profile
fi
```

In this example, assume that the path of the System V habitat is /usr/opt/s5 as reflected by the contents of /etc/svid2path and that your login directory is /usr/users/xxx. When you display the PATH after logging in with the preceding .profile file, the result would show that the path to the System V habitat has been prepended to the PATH set in the third line of the .profile file as follows:

```
% echo $PATH  Return
/usr/opt/s5/bin:/usr/opt/s5/sbin:/usr/users/xxx/bin:/usr/lib:/bin
```

Hence, when you issue a shell command, the System V habitat is searched first. If the command is not found, the specified paths are searched.

# 9.3 Compatibility for Shell Scripts

Compatibility for your shell scripts is achieved by altering your shell's PATH environment variable (as explained in Section 9.1). Therefore, the System V habitat is searched before the default system locations. If your PATH variable is set for the System V habitat, your scripts are System V compatible regardless of whether you use the C shell or the Bourne, Korn, or POSIX shell.

# 9.4 System V Habitat Command Summary

Table 9-1 summarizes the behavior of user commands in the System V habitat that have options or features that differ from the default system versions. For a complete explanation of the commands in the habitat, refer to the reference page for each command.