# CERTIFICATION OBJECTIVE 3.02

# Standard Command Line Tools

You can add standard output to the end of an existing file with a double redirection arrow with a command such as `ls >> filelist`. If you believe that a particular program is generating errors, redirect the error stream from it with a command like the following:

```
# program 2> err-list
```

> **exam watch** Command redirection symbols like >, >>, 2>, 2>&1, and | are associated with the "input/output redirection" objective in the RHCSA exam objectives.

While newer Linux users may prefer to use the GUI, the most efficient way to administer Linux is from the command line interface. While excellent GUI tools are available, the look and feel of those tools varies widely by distribution. In contrast, if you know the standard command line tools, you'll be able to find your way around every Linux distribution.

> **exam watch** This section covers only the most basic of commands available in Linux. It describes only a few capabilities of each command. Nevertheless, it allows you to "issue commands with correct syntax," as described in the RHCSA objectives.

Two basic groups of commands are used to manage Linux files. One group helps you get around Linux files and directories. The other group actually does something creative with the files. Remember, in any Linux file operation, you can take advantage of the HISTORY (this is capitalized because it's a standard environment variable) of previous commands, as well as the characteristics of command completion, which allow you to use the TAB key almost as a wildcard to complete a command or a filename, or give you the options available in terms of the absolute path.

Almost all Linux commands include switches, options that allow you to do more. Few are covered in this chapter. If you're less familiar with any of these commands, use their man pages. Study the switches. Try them out! Only with practice, practice, and more practice can you really understand the power behind some of these commands.