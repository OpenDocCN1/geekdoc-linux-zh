
The following is a sample entry from /etc/passwd on my system:

```
ranga:x:500:100:Sriranga Veeraraghavan:/home/ranga:/bin/bash
```

The entry is composed of several fields, each separated from the other fields by a colon, :. Later chapters will explain the information stored in each field. For now, only the last two fields are important. The last field stores the shell associated with the account. The second from the last field stores the home directory for the account. The home directory is where you first start out after logging in. In some documentation, you will see home directories denoted by a tilde, ~, or a tilde followed by a slash, ~/ . In the previous example, the shell is /bin/bash and the home directory is /home/ranga. Your shell and home directory will most likely be different.

In most cases, the system administrator will assign you the default shell for a particular version of UNIX. In some cases, there are two defaults and the system administrator can choose between them based on his personal preferences.

The default shells for some common versions of UNIX are as follows:

- Solaris uses Bourne shell or C Shell.
- HP-UX uses POSIX shell.
- BSD uses Korn Shell or C Shell.
- Mac OS X uses Z Shell or C Shell.
- Linux uses the Bourne Again Shell.

For the sake of brevity, we assume that you have been assigned Bourne shell, Korn Shell (ksh), Bourne Again Shell (bash), or Z Shell (zsh) as your shell.

## Shell Modes and Initialization

In this section, we will first discuss the startup procedure for the various Bourne-type shells, and then we will examine the different modes of execution for a shell.

## Initialization Procedures

After you log in, a shell is executed on your behalf. When this shell starts executing, it is uninitialized. In this state, several parameters required for its proper operation are not defined. The shell undergoes a process called initialization that defines these parameters. The steps and files involved in initialization are different in each shell, so we will examine the process used by each of the Bourne-type shells individually. In general each of the shells uses default or system-wide configuration files located in the /etc directory along with a set of personal configuration files located in your home directory.

## Bourne Shell

Bourne shell initialization has four steps and involves the initialization files (also called init files) `/etc/profile` and `.profile`. The process is as follows:

- 1. The shell checks to see whether the file `/etc/profile` exists.
- 2. If it exists, the shell reads it; otherwise, the shell skips it.
- 3. The shell checks to see whether the file `.profile` exists in your home directory.
- 4. If it exists, the shell reads it; otherwise, the shell skips it.

After these steps have been performed, the prompt is displayed. The default prompt for Bourne shell is `$` (a dollar sign followed by a space).

## Korn Shell

Korn Shell (`ksh`) closely resembles Bourne shell initialization. It has six steps and involves the init files `/etc/profile`, `.profile`, and `.kshrc`:

- 1. ksh checks to see whether the file `/etc/profile` exists.
- 2. If it exists, ksh reads it; otherwise, ksh skips it.
- 3. ksh checks to see whether the file `.profile` exists in your home directory.
- 4. If it exists, ksh reads it; otherwise, ksh skips it.
- 5. ksh checks to see whether the file `.kshrc` exists in your home directory.
- 6. If it exists, ksh reads it; otherwise, ksh skips it.

After these steps have been performed, the prompt is displayed. The default prompt for `ksh` is `$` (a dollar sign followed by a space).

## Bourne Again Shell

Bourne Again shell (bash) initialization is a bit longer than Korn shell and Bourne shell initialization. It has eight steps and involves the init files `/etc/profile`, `.bash_profile`, `.bash_login`, and `.profile`:

- 1. bash checks to see whether the file `/etc/profile` exists.
- 2. If it exists, bash reads it; otherwise, bash skips it.
- 3. bash checks to see whether the file `.bash_profile` exists in your home directory.
- 4. If it exists, bash reads it; otherwise, bash skips it.
- 5. bash checks to see whether the file `.bash_login` exists in your home directory.
- 6. If it exists, bash reads it; otherwise, bash skips it.
- 7. bash checks to see whether the file `.profile` exists in your home directory.
- 8. If it exists, bash reads it; otherwise, bash skips it.

After these steps have been performed, a prompt is displayed. The default prompt for bash is bash$ (the string bash$ followed by a space).

## Z Shell

Z shell (zsh) initialization is quite long and does not resemble the initialization process of the other shells. It has 16 steps and involves the init files /etc/zshenv, .zshenv, /etc/zprofile, .zprofile, /etc/zlogin, and .zlogin:

- 1. zsh checks to see whether the file /etc/zshenv exists.
- 2. If it exists, zsh reads it; otherwise, zsh skips it.
- 3. zsh checks to see whether the file .zshenv exists in your home directory.
- 4. If it exists, zsh reads it; otherwise, zsh skips it.
- 5. zsh checks to see whether the file /etc/zprofile exists.
- 6. If it exists, zsh reads it; otherwise, zsh skips it.
- 7. zsh checks to see whether the file .zprofile exists in your home directory.
- 8. If it exists, zsh reads it; otherwise, zsh skips it.
- 9. zsh checks to see whether the file /etc/zshrc exists.
- 10. If it exists, zsh reads it; otherwise, zsh skips it.
- 11. zsh checks to see whether the file .zshrc exists in your home directory.
- 12. If it exists, zsh reads it; otherwise, zsh skips it.
- 13. zsh checks to see whether the file /etc/zlogin exists.
- 14. If it exists, zsh reads it; otherwise, zsh skips it.
- 15. zsh checks to see whether the file .zlogin exists in your home directory.
- 16. If it exists, zsh reads it; otherwise, zsh skips it.

After these steps have been performed, a prompt is displayed. The default prompt for zsh is host%. Here host is the hostname of your system. For example, on a system named nars, the default zsh prompt would be nars%.

## Initialization File Contents

Usually a shell's init files are quite short. The purpose of these files is to provide a complete working environment with as little overhead as possible. In this section, we will look at the basic settings required for Bourne shell. If you are using a different shell, you can put these settings into an init file used by that shell.

The init file .profile contains all of your shell initialization settings. You can add as much customization information as you want to this file. The minimum set of information that you need to configure includes

- A list of directories in which to locate commands
- A list of directories in which to locate manual pages for commands

## Setting PATH

When you type the command,

```
$ date
```

The shell has to locate the command date before it can be executed. The PATH variable specifies the directories in which the shell should look for commands. The most basic setting is as follows:

```
PATH=/bin:/usr/bin
```

Each of the individual entries separated by the colon character, :, should be directories. Directories are discussed in Chapter 4.

If you request the shell to execute a command and it cannot find it in any of the directories given in the PATH variable, a message similar to the following appears:

```
$ hello
hello: not found
```

## Setting MANPATH

In UNIX, online help has been available since the beginning. The next section, “Getting Help,” discusses how to access the online help using the man command. In order for this command to work properly, you have to tell the shell where the help pages are located. This information is specified using the MANPATH. A common setting is

```
MANPATH=/usr/man:/usr/share/man
```

Similar to the path, each of the individual entries separated by the colon character, :, are directories.

When you use the man command to request online help, it searches every directory given in the MANPATH for an online help page corresponding to the topic you requested. For example, the command

```
$ man who
```

looks for the online help page corresponding to the who command. If this page is found, it is displayed.
