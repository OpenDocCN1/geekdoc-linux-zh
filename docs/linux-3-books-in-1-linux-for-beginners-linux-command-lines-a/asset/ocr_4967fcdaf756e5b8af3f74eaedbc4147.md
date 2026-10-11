```
`[gha@localhost ~]# which ls
ls='ls --color=auto'
  /bin/ls`
```

The which command works well for executable programs only and not for built-ins or alias that are mostly substitutes for executable programs. When you try to use the which command on shell built-in, you get either no response or a big error message.

```
`[gha@localhost ~]# which help
/usr/bin/which: no help in (/usr/local/sbin:/bin:/sbin:/usr/bin:/usr/local/bin)`
```

# ## Documentation of Commands

You can take a step further and fish out the available documentation in the system for each type of command.

# ### The help command

Bash shell has a built-in help facility for shell built-ins. If you want to use it, you can type help and the name of the shell built-in. See the following example.

```
`[gha@localhost ~]$ help cd
cd: cd [-L|P [-e]] [-@] [dir]`
```

Change the shell working directory.

Change current directory to DIR. The default DIR is the HOME Shell variable’s value.

The CDPATH variable is used to define the search path leading to the directory where DIR is. CDPATH indicates alternative file names by using a colon (:) to separate them. A null name indicates the current directory, and where a slash (/) precedes a directory name, then CDPATH isn’t used.

The details are longer than I have mentioned here. I cut it down to save space. You can type the command on the terminal and see how the help command can help you out when you get stuck as you operate the Linux operating system. When you see square brackets in the description of a command’s syntax, you should keep in mind that they indicate only optional items. If you see a vertical bar character in the description, it denotes mutually exclusive items. Some executable programs support the --help option. When you apply