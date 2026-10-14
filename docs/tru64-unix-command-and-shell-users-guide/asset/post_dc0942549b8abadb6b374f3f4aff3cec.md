
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

## 9.3 Compatibility for Shell Scripts

Compatibility for your shell scripts is achieved by altering your shell's PATH environment variable (as explained in Section 9.1). Therefore, the System V habitat is searched before the default system locations. If your PATH variable is set for the System V habitat, your scripts are System V compatible regardless of whether you use the C shell or the Bourne, Korn, or POSIX shell.

## 9.4 System V Habitat Command Summary

Table 9-1 summarizes the behavior of user commands in the System V habitat that have options or features that differ from the default system versions. For a complete explanation of the commands in the habitat, refer to the reference page for each command.

**Table 9-1: User Commands Summary**

| Command | System V Behavior |
|---|---|
| chmod(1) | Ignores the umask value when the who string is omitted, behaving as though a is the who value when you use the symbolic form of this command. |
| df(1) | Accepts the -t option, which prints space totals, and accepts an optional file system name or device name. |
| ln(1) | Accepts the -f option, which silently removes existing destination pathnames before creating the specified link. |
| ls(1) | Produces multicolumn output only if the -C option is specified. Also, the -s option causes file sizes to be reported in 512 byte units instead of 1024 byte units. |
| mailx(1) and Mail(1) | Includes the capabilities of the System V mailx command. |
| sum(1) | Uses the word-by-word algorithm by default; uses the byte-by-byte algorithm if the -r option is specified. The default use of the checksum algorithms for the System V sum command is the reverse of the default system version of the sum command. |
| tr(1) | Includes the -A option whenever you specify the -c option. The -A option causes only the characters in the octal range of 1 to 377 to be complemented. |

## 10

## Obtaining Information About Network Users and Hosts

This chapter describes how to find information about local and remote users and hosts before you begin communication or file transfer tasks. The commands described in this chapter will enable you to:

- Learn about your own network connection (who am i command, Section 10.1)
- Determine who is currently logged in to the local system and from where they are logged in (who command, Section 10.1)
- Find additional information about another user, if available; for example, full name, office location, phone number, projects, or plans (finger command, Section 10.2.1)
- Determine whether a user can be reached using either the talk or write commands (finger command, Section 10.2.1 and Section 10.2.2)
- Analyze and sort information about remote host usage (uptime command, Section 10.3)
- Determine who is currently logged in to a remote host (rwho command, Section 10.4)
- Determine whether a remote host is on line (ping command, Section 10.5)

### Note

> The commands described in this chapter are, like all TCP/IP operations, subject to the security features on the local and remote hosts. If they do not work as stated here or in the related reference pages, see your system administrator.

## 10.1 Identifying Users on the Local Host

When you log in to a host computer by providing a user name and password, you have a unique identity. To verify this information for your own network connection, you can use a version of the who command called who am i to display the following information about you:
