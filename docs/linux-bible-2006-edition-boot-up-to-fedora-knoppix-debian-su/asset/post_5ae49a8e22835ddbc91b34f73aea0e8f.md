
# 34 Part I Linux First Steps

Many features of the original csh, such as command-line editing and its history mechanism, are included in tcsh as well as in other shells. While you can run both csh and tcsh on most Linux systems, both commands point to the same executable file. In other words, starting csh actually runs the tcsh shell in compatibility mode.

## Using ash

The ash is a lightweight version of the Berkeley UNIX shell. It doesn't include many of the sh shell's basic features, and is missing such features as command-histories. Kenneth Almquist created the ash.

The ash is a good shell for embedded systems that have fewer resources available. The ash shell is about one-sixth the size of bash (around 100k versus 680k for bash). Because of cheaper memory prices these days, many embedded and small Linux systems have enough space to include the full shell.

## Using ksh

The ksh was created by David Korn at AT&T Bell Labs and is the predecessor of the sh shell. It became the default and most commonly used shell with UNIX systems. The open source version of ksh was originally available in many rpm-based systems (such as Fedora and Red Hat Enterprise Linux). David Korn released the original ksh as open source, so you can look for it as part of software in Linux systems.

## Using zsh

The zsh shell is another clone of the sh shell. It is POSIX-compliant but includes some different features such as spell checking and command editing. Mac OS use zsh as the default although bash is used by default.

## Exploring the Shell

Once you have access to a shell in Linux, you can begin by typing simple commands. The "Using the Shell in Linux" section later provides more details about options, arguments, and environment variables. For the time being, the following sections will help you poke around.

## Running Commands from the Shell

If you don't like your default shell, simply type the name of the shell you want to try out. To change your shell permanently, use the usermod command. For example, to change your shell to csh for the user named chris, type:

```bash
usermod -s /bin/csh chris
```

## Checking Your Login Session

When you log in to a Linux system, Linux views you as having a particular identity which includes your username, group name, user ID, and group ID. Linux also tracks when you logged in, how long you have been idle, and where you logged in. To find out your identity use the id command as follows:

```bash
$ id
uid=501(chris) gid=105(sales) groups=105(sales),4(adm),7(lpd)
```

In this example, the username is chris (uid=501). The primary group for chris is sales (gid=105). The user chris also belongs to other groups adm (4) and lpd (7). These names and numbers represent the permissions that chris has to access resources.

You can see information about your current login session using the who command. The -u option adds information about idle time and the process and has a header that is printed:

```bash
$ who -u
NAME TIME IDLE PID COMMENT
chris tty Jan 13 20:57 .
```

The output from who shows that the user is logged in on tty (which), the login session began at 20:57 on January 13. The idle time shows how long the shell has been open without any command being typed (the dot indicates that it is currently active). PID shows the process ID of the user. COMMENT shows the name of the remote computer the user logged in from, or the name of the local if you are using a Terminal window (such as :0).

## Checking Directories and Permissions

Associated with each shell is a location in the Linux file system known as the current or working directory. Each user has a directory that is identified as the user's home directory. When you first log in to Linux, you begin with your home directory as the current directory.

When you want to open or save a file, your shell uses the current directory as the point of reference. Simply provide a filename when you save a file, and it is placed in the current directory (relative path). Alternatively, you can identify a file by its relation to the current directory (relative path), or you can ignore the current directory and identify a file by the full directory hierarchy (absolute path). The structure and use of the file system is described in detail later in this chapter.

To find out your current directory is, type the pwd command:

```bash
$ pwd
/usr/bin
```

In this example, the current working directory is /usr/bin. To find the name of your home directory, use the echo command followed by the $HOME variable:

```bash
$ echo $HOME
/home/chris
```

Here the home directory is /home/chris. To get back to your home directory, just type the change directory (cd) command. (Although cd followed by a directory name changes the current directory to the directory you choose, typing cd with no directory name takes you to your home directory):

```bash
$ cd
```

> **Note:** Instead of typing $HOME, you can use the tilde (~) to refer to your home directory. So, to return to your home directory, you could simply type: `cd ~`

To list the contents of your home directory, either use the full path to your home directory or the ls command without a directory name. Using the -a option enables you to see the hidden files (dot files) as well as all other files. With the -l option you can see a long, detailed list of each file. (You can combine multiple single-letter options after a single dash, for example, -la).

```bash
$ ls -la /home
total 16
drwxr-xr-x 2 chris sales 4096 Jan 13 20:57 .
drwxr-xr-x 4 root root 4096 Jan 13 20:00 ..
-rw-r--r-- 1 chris chris  920 Jan 13 20:57 .bash_history
-rw-r--r-- 1 chris chris 1200 Jan 13 20:57 .bash_profile
-rw-r--r-- 1 chris chris  800 Jan 13 20:57 .bashrc
-rw-r--r-- 1 chris chris 1500 Jan 13 20:57 .bashlogout
```
