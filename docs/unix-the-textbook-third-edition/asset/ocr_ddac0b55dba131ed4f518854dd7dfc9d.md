Each UNIX system has an initial system start-up file, usually named .profile in Solaris and .login in PC-BSD. This file contains the initial settings of important environment variables for the shell and some other utilities. In addition, hidden files for specific shells are executed when you start a particular shell. Known as the shell start-up files, they are .cshrc for C shell and .bashrc for Bash. These hidden files are initially configured by the system administrator for secure use by all users. Table 2.6 lists some important environment variables common to Bash, Bourne, Korn, and C shells; the C shell variable name, where applicable, is in lowercase following the Bash, Bourne, and Korn shell variable name. Note that your system administrator may not have set some of these variables, such as ENV.

The following in-chapter exercises let you view the settings of your environment variables. They assume that you are initially running the Bourne or Korn shells. If you aren’t, run either of those shells as described in Section 2.8.3 and then do the exercises.

# EXERCISE 2.11

At the default login shell prompt for your system, type `set | more` and then press <Enter>. What is displayed on your screen? Identify and list the settings for all the environment variables shown in Table 2.6.

# EXERCISE 2.12

At the shell prompt, type `csh` or `bash` depending on your default system login shell, and then press <Enter>. Next, type `setenv | more` and then press <Enter>. Identify and list the settings for all the environment variables shown in Table 2.6.

In addition to the shells, several other programs have their own hidden files. These files are used to set up and configure the operating environment within which these programs execute. We discuss some of these hidden files in Chapters 4 and 5. They are called hidden files because when you list the names of files contained in your home directory—for example, with the `ls -l` command and option (see Chapter 4)—these files do not appear on the list. The hidden file names always start with a period (.), such as .login.

# TABLE 2.6 Shell Environment Variables

| Environment Variable | What It Affects |
|---|---|
| CDPATH, cdpath | The alias names for directories accessed with the cd command |
| EDITOR | The default editor used in programs such as the e-mail program Elm |
| ENV | The path along which UNIX looks to find configuration files |
| HOME, home | The name of the user’s home directory when the user first logs on |
| MAIL, mail | The name of the system mailbox file |
| PATH, path | The directories that a shell searches to find a command or program |
| PS1, prompt | The shell prompt that appears on the command line |
| PWD, cwd | The name of the current working directory |
| TERM | The type of console terminal being used |