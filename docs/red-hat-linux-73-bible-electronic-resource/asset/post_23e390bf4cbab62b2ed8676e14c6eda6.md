
In the above code, `hostname` is replaced by the computer that you want to login to. You can use any host name that is in your `/etc/hosts` file or that can be obtained through DNS. Once you have started `rlogin`, you can use any of the following key sequences:

- `~.` — Exit. This causes the login program to exit (ungracefully). I use this option if the remote shell is hung or if I get stuck at the login prompt (from a forgotten password or logged into the wrong system).
- `~Ctrl+Shift+z` — Suspend. (Press Ctrl and Shift while pressing z.) This puts the current rlogin session in the background, returning you to a local shell command line. To return to the suspended session, type `fg`.

### Using rcp for remote copies

The `rcp` command is handy for copying one file or a whole directory structure of files from one computer to another. It is quicker than `ftp` because you don't have to start a session and login before you copy a file. However, because `rcp` doesn't prompt for a password, it requires that you configure `rhosts` authentication (discussed above) for it to work.

To copy a file from one computer to another, use the following command:

```bash
$ rcp fileX maple:/home/mike
```

That command would copy the file (`fileX`) to `/home/mike` on the computer named `maple`. You could also take a file from another computer by typing the following:

```bash
$ rcp maple:/home/mike/fileZ .
```

That command would copy the file (`fileZ`) from `/home/mike` on `maple` and place it in the current directory (`.`).

Perhaps the most useful option for the `rcp` command is the `-r` option. The `-r` option enables you to copy all the files in a directory structure from one computer to another. This can provide an easy way of backing up a large area of data in one command. Here is an example:

```bash
$ rcp -r /a maple:/backup/pine
```

The previous example is one that I use. I store all my software and data files in the directory `/a`. If I want to do a quick backup or if I want to reinstall Red Hat Linux, I can copy all of my data and software to `maple`, reinstall the local system, then `rcp` the files back again. This command creates a directory on `maple` in a directory called `/backup/pine/a`. That directory can contain hundreds of files and subdirectories.

### Using rsh for remote execution

While previous commands, such as `rcp` and `ftp`, can help you share files among computers on your network, `rsh` lets you share the processors. With `rsh`, it is simple to ask that a command be run on any computer for which you have `rhosts` access. Likewise, you can have the command's output printed on your screen, directed to a local file, or to a remote file.

Here are four examples of the `rsh` command:

```bash
$ rsh spruce who
$ rsh maple "tail -f /var/log/messages"
$ rsh pine "man rlogin" >> /tmp/rlman
$ rsh fir "uname -a" ">>" /tmp/name
```

In the first example, the `who` command is run on the remote computer named `spruce` and the output appears on the local screen. The second example runs the `tail -f` command to display messages as they arrive in the `/var/log/messages` file on `maple`. (This is a good way to remotely monitor log files in one quick command line.) The next command runs the `man` command to output the `rlogin` man page and outputs the results to the `/tmp/rlman` file on the local system. In the final example, the `uname -a` command runs on `fir`, but by quoting the arrows, the output is sent to the `/tmp/name` file on the remote computer, rather than the local one.

## Summary

Most use of the World Wide Web centers on the Web browser. Mozilla and Netscape are popular browsers with Red Hat Linux, and are accessible from a button on your desktop. The e-mail program that comes with Mozilla, called Mozilla Mail, provides most everything needed for reading, sending, and managing your mail. To read newsgroups, you can use Netscape Messenger. Text-based newsreaders are also available.

To pass data around freely between trusted hosts, you can use a set of commands sometimes referred to as "r" commands. Commands such as `telnet` (for remote login) and `ftp` (for remote file copying) are also available with Red Hat Linux. There are also improved programs for remote login and file copy, such as `ssh` and `ncftp`, respectively.

# Part III: Administering Red Hat Linux

## Chapter 10: Understanding System Administration

## Chapter 11: Setting up and Supporting Users

## Chapter 12: Automating System Tasks

## Chapter 13: Backing up and Restoring Issues

## Chapter 14: Computer Security Issues

# Chapter 10: Understanding System Administration

### In This Chapter

- Using the root login
- Administrative commands, configuration files, and log files
- Getting to know your system
- Graphical administrative interfaces
- Working with the file system
- Working with hardware devices
- Monitoring system performance

Red Hat Linux, like other UNIX systems, was intended for use by more than one person at a time. Multiuser features allow many people to have accounts in Red Hat Linux, with their data kept secure from others. Multitasking allows many people to use the computer at the same time. Sophisticated networking protocols and applications make it possible for a Red Hat Linux computer to extend its capabilities to network users and computers around the world. The person assigned to manage all of this stuff is referred to as the *system administrator*.

Even if you are the only person using a Red Hat Linux system, system administration is still set up to be separate from other computer use. To do most tasks, you need to be logged in as the root user (also referred to as the super user). Other users cannot change, or in some cases, even see some of the configuration information for a Red Hat Linux system. In particular, security features such as passwords are protected from general view.

General principles of Red Hat Linux system administration are described in this chapter. In particular, this chapter covers some of the basic tools you need to administer your Red Hat Linux system. It also helps teach you how to work with file systems and monitor the setup and performance of your Linux system.

## Using the root Login

The root user has complete control of the operation of your Red Hat Linux system. That user can open any file or run any program. The root user also installs applications and adds accounts for other people who use the system.

When you first install Red Hat Linux, you should have added a password for the root user. You need to remember and protect this password. You will need it to log in as root or to obtain root permission while you are logged in as some other user.

The home directory for the root user is `/root`. That and other information associated with the root user account is located in the `/etc/passwd` file. Here is what the root entry looks like in the `/etc/passwd` file:

```text
root:x:0:0:root:/root:/bin/bash
```

This shows that for the user named root, the user ID is set to 0 (root user), the group ID is set to 0 (root group), the home directory is `/root`, and the shell for that user is `/bin/bash`. You can change the home directory or the shell used, if you like, by simply editing the values in this file.

> **CROSS-REFERENCE:** See the section on setting up users in Chapter 11 for further information about the `/etc/passwd` file.

Among the defaults that are set for the root user are aliases for certain dangerous commands. Aliases for the `rm`, `cp`, and `mv` commands allow those commands to be run with the `-i` option. This prevents massive numbers of files being removed, copied, or moved by mistake. The `-i` option causes each deletion, copy, or move to prompt you before the actual change is made.

## Becoming Super User (The su Command)

Though the normal way to become the super user is to log in as root, sometimes that is not convenient. For example, you may be logged into a regular user account and just want to make a quick administrative change to your system without having to log out and log back in. Or, you may need to log in over the network to make a change to a Linux system but find that the system doesn't allow root users in from over the network (a common practice).

The answer is that you can use the `su` command. From any Terminal window or shell, you can simply type:

```bash
$ su
Password: *****
#
```

When you are prompted, type in the root user's password. The prompt for the regular user (`$`) will be changed to the super user prompt (`#`). At this point, you have full permission to run any command and use any file on the system. However, one thing that the `su` command doesn't do
