
# Part IV: Working with Alternative Shells

Most Korn shell implementations (including those found in Linux distributions) use the ksh93 shell. Older Sun Solaris systems used a proprietary modified version of the ksh88 shell, but newer Oracle Solaris systems use the standard ksh93 shell for scripting and the Bash shell for the command line. Because the Korn shell available in Linux distributions uses the open source ksh93 shell, that's the shell that's covered in this chapter.

> **Note**
> The ksh93 shell is also referred to as the Enhanced Korn shell in some Linux distributions and in some UNIX systems (such as IBM's AIX operating system).

There is one other version of the Korn shell you may run into in the Linux environment. During the time when the original Korn shell was proprietary software, a public domain version of the Korn shell (called the pdksh shell) was developed. The pdksh shell has most of the same features as the ksh88 shell but is missing the advanced mathematical features found in the ksh93 shell.

The next section explains how to install and use the ksh93 shell in both Debian and Red Hat-based Linux distributions.

## Installing the ksh93 Shell

Most Linux distributions don't install the ksh93 shell by default, but it's easy to install and use. There are packages in both the Debian .deb and Red Hat .rpm formats. Unfortunately, the package names are often just called ksh instead of ksh93.

To install the ksh93 shell in Ubuntu, just use this command:

```bash
$ sudo apt install ksh
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  ksh93u+m
Suggested packages:
  bfont-support
The following NEW packages will be installed:
  ksh ksh93u+m
0 upgraded, 2 newly installed, 0 to remove and 68 not upgraded.
Need to get 902 kB of archives.
After this operation, 3,248 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
...
```

And for the Rocky Linux installation, the command is as follows:

```bash
$ sudo dnf install ksh
Rocky Linux 9 - BaseOS 4.7 kB/s | 4.1 kB 00:00
Rocky Linux 9 - AppStream 431 B/s | 4.5 kB 00:10
Rocky Linux 9 - Extras 541 B/s | 2.9 kB 00:05
Dependencies resolved.
===========================================================================================================================================
 Package Architecture Version Repository Size
===========================================================================================================================================
Installing:
ksh x86_64 3:1.0.6-7.el9_6.1 appstream 879 k
Transaction Summary
Install 1 Package
Total download size: 879 k
Installed size: 3.0 M
Is this ok [y/N]:
```

That's all there is to it! To start the ksh93 shell, just enter the ksh command at the Bash command prompt:

```bash
[richar@rocky9 ~]$
 ksh --version
version sh (AT&T Research) 93u+m/1.0.6 2023-06-13
$
```

If you want to assign the ksh93 shell as the default shell for a user account, use the chsh command with the -s option:

```bash
$ sudo chsh -s /bin/ksh test1
Changing shell for test1.
Shell changed.
$
```

The following section describes the different parts of the ksh93 shell.

## Understanding Parts of the ksh93 Shell

Since the ksh93 shell is based on the Bourne and C shells, you'll see lots of similarities between it and the Bash and tcsh shells. This section describes the individual features of the ksh93 shell, including the command line parameters, environment variables, and built-in commands.

### Command line parameters

As with other shells, the Linux ksh93 shell utilizes command line parameters to define how it behaves, both as an interactive shell and as a shell scripting shell. Table 25.1 lists the command line parameters you can use when starting a new ksh93 shell session.

**TABLE 25.1 The ksh93 Command Line Parameters**

| Parameter | Description |
| :-- | :-- |
| -a | Automatically exports shell variables. |
| -A | Assigns values from the command line arguments to the specified array variable. |
| -b | Displays job completion messages as soon as jobs change state. |
| -B | Enables brace pattern field generation. |
| -c | Reads commands from the first argument. |
| -C | Prevents redirection from truncating existing files. |
| -D | Doesn’t execute commands. Displays double-quoted strings that are preceded by a dollar sign. |
| -e | If a command has a non-zero exit status, exits the shell. |
| -f | Disables pathname expansion. |
| -G | Enables recursive pathname expansion when using wildcard characters \*\*. |
| -H | Enables command history expansion using the ! character. |
| -k | All variable assignment arguments are placed in the command environment. |
| -m | Background jobs run as a separate process group. |
| -n | Reads commands and checks for errors, but doesn’t execute them. |
| -o | Sets default shell options. |
| -p | Disables processing the $HOME/.profile file. |
| -r | Starts the shell as a restricted shell. |
| -s | Sorts the positional parameters lexicographically. |
| -u | Treats unset parameters as an error when substituting. |
| -v | Displays shell input lines as they are read. |
| -x | Displays commands and their arguments as they are executed. |

The ksh93 command line parameters are pretty similar to the Bash shell. Besides the command line parameters, you can customize the shell behavior using the -o command line parameter. There are quite a few shell options you can set with this parameter:

- allexport: Automatically exports variables.
- bgnice: Runs all background jobs at a lower priority.
- braceexpand: Enables brace pattern field generation.
- emacs: Uses emacs editor mode for command line editing.
- errexit: Exits the shell if a command generates a non-zero exit status.
- ignoreeof: The shell doesn’t exit on an EOF character.
- markdirs: All directory names resulting from file generation use a trailing slash.
- monitor: Background jobs run as a separate process group.
- noclobber: Prevents redirection from overwriting files.
- noexec: Reads commands and displays errors, but doesn't execute them.
- noglob: Disables filename expansion.
- nolog: Doesn't save functions in history log.
- notify: Displays new status of jobs when they change status.
- nounset: Treats unset parameters as an error.
- pipefail: Pipelines won't complete until all components have completed.
- privileged: Disables processing of $HOME/.profile file.
- trackall: Each command becomes a tracked alias.
- verbose: Displays commands as the shell reads them.
- vi: Uses vi editor mode for command line editing.
- viram: Processes each character as it's typed in vi editor mode.
- xtrace: Displays commands as the shell executes them.

You can set multiple command line options on the command line to set multiple features for the shell at once. Also, note that many of the command line options are duplicated as command line parameters. You can use either type to set the command line features.

### Default files

When you use the ksh93 shell as a login shell, it reads commands from two files:

- /etc/profile
- $HOME/.profile

You should store commands that are executed by all users in the /etc/profile file, while commands for individual users should be stored in the appropriate $HOME/.profile file.

### Environment variables

The ksh93 shell uses environment variables to set features and provide information about the shell environment. Table 25.2 shows the default environment variables available in the ksh93 shell.

| Variable | Description |
|---|---|
| CDPATH | The search path for the cd command. |
| COLUMNS | The terminal width in characters for edit mode. |
| EDITOR | The default editor used for command line editing. |
| ENV | Defines a file used for specifying parameter expansion, command substitution, and arithmetic substitution (commonly $HOME/.kshrc). |
| FIGNORE | The set of filenames ignored when performing filename matching. |
