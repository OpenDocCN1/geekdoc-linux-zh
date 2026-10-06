# Chapter 2 + Running Commands from the Shell

$ echo I am $[2006 - 1957] years old.
Iam 49 years old.

The shell interprets the arithmetic expression first (2005 - 1957), and then passes information to the echo command. The echo command displays the text, with the results of the arithmetic (48) inserted.

Here's an example of the other form:

```
$ echo "There are $(ls | wc -w) files in this directory."
There are 14 files in this directory.
```

This lists the contents of the current directory (ls) and runs the word count to count the number of files found (wc -w). The resulting number (14 in this case) is echoed with the rest of the sentence shown.

# Expanding Environment Variables

Environment variables store information within the shell can be expanded using the dollar sign ($) metacharacter. When you expand an environment variable on a command line, the value of the variable is printed instead of the variable name itself:

```
$ ls -l $BASH
-rwxr-xr-x root 625516 Dec 5 11:13 /bin/bash
```

Using $BASH as an argument to ls -l causes a line listing of the bash command to be printed. The following section discusses environment variables.

# Creating Your Shell Environment

You can tune your shell to help you work more efficiently. Your prompt can provide pertinent information each time you press Enter. You can set aliases to save your keystrokes and permanently environment variables to suit your needs. To make each change occur when you start a shell, add this information to your shell configuration.

# Configuring Your Shell

Several configuration files support how your shell behaves. Some of the files are executed for every user and every shell, while others are specific to the user who creates the configuration file. Table 2-6 shows the files that are of interest to anyone using the bash shell in Linux.

To change the /etc/profile or /etc/bashrc files, you must be the root user. Users can change the information in the $HOME/.bash_profile, $HOME/.bashrc, and $HOME/.bash_logout in their own home directories.