
## 1.3 SUMMARY

The information in this chapter should provide administrators with pointers of how to gather information about the configuration of environment variables and how to set the system time, if needed; how to investigate the number of superusers, should there be more than one; and how to create a secure location for root to store sensitive information concerning the system. Furthermore, this chapter discussed how to display statistics about running processes and the mail system and closed with a short discussion about where additional software should be installed.

## 2 Working on *NIX

### In This Chapter
- Executables on *NIX
- Shell Scripts Step by Step
- Perl Scripts
- Automation

Compared to the “other” dominant operating system, *NIX uses a different approach regarding programming and system tasks. *NIX supplies the user with literally dozens of small programs capable of doing one or more things “right.”

The programs talk to each other via defined interfaces, thus minimizing the risk of breaking something if one of them changes or gets expanded capabilities. You are able to choose your tools and chain them together to achieve what you have in mind, regardless of whether the small program in question is simply a script or a binary. Indeed, many commands are actually shell or Perl scripts, and, given the flexibility of this approach, you can study and re-use them or exchange them completely with something you write yourself. The latter approach is rarely necessary, but comes in handy if you need to take care of a very special case.

## 2.1 EXECUTABLES ON *NIX

How does the *NIX-system “know” which files are executable? Why isn’t every user allowed to execute all programs on the system? How does the system make sure that programs don’t overwrite data belonging to another process? These questions will be answered in the following sections.

### 2.1.1 Why Is a Program Executed?

Contrary to other operating systems, *NIX features a tight control system and runs a couple of checks before a program gets executed. The system checks first whether the user, or the calling process for that matter, has the right to execute the program, if it is marked as executable at all. If this check goes through and the program tries to create a file, the system makes sure the user has the right to create that file in this very location. The same holds true for creating files in random access memory (RAM). Given this chain of security checks, it is almost impossible to overwrite important files belonging to the system or another user. If you are logged in as root, some of the restrictions don’t apply, though. So, if you execute a program or script while logged in as root, make sure the outcome is what you intended to do in the first place—especially with commands like rm (remove), which, when executed in the superuser context, rely on your judgment and proceed without asking.

> Even if some seasoned *NIX administrators will tell you otherwise, the author has seen this firsthand—some *NIX brands don’t mind if someone tries to remove the kernel from the hard disk! To be precise, they don’t mind as long as the system will not be rebooted. Admittedly, the author saw this happen on an older system, but still, there was no warning; the kernel was simply removed. Double-check while working as root.

### 2.1.2 What Is #!?

When browsing executable files like shell or Perl scripts, you inevitably encounter lines like #!/bin/sh or #!/usr/bin/perl -w. Take a look at Listing 2.1.

### LISTING 2.1 The First Line of an Executable Script

```
erik@unixhost:~> more netatalk-config
#!/bin/sh
# netatalk-config
af_libs=
af_cflags=
```

```
prefix=/usr
exec_prefix=$(prefix)
...
```

These lines occur only in line one of the script and are called shebangs. If a file containing text is marked as executable, line one should contain the interpreter, including the path, needed to run the file as a program. If this prerequisite is fulfilled, the file can be executed either from the command line or launched from the window manager of choice. This could be a portability issue, though; for example, if the program perl is not in the /usr/bin directory on a system, the script will not execute, for obvious reasons. The shebang is a shortcut for typing perl myscript.pl, thus enabling scripts to behave like programs.

### 2.1.3 Why Use ./ ?

If you want to make sure to launch the right program or script, it is always advisable to use either a full pathname like /usr/bin/ls or the shortcut ./<program> if the current location of $PWD is already the directory the command or script resides in— for example, ./ls is obviously just an example, but just in case you try to create a better version of the command, it makes sense to control which one is executed. While you are testing the new program or script, chances are that the current directory is already the directory it was built or written in. The shortcut ./ implies using the current path ($PWD) to search for the program to be executed, instead of traversing the contents of $PATH to find the executable named on the command line. Another use of the shortcut is to make use of untainted binaries executed from another location like a CD-ROM while working on a compromised or malfunctioning system.

## 2.2 SHELL SCRIPTS STEP BY STEP

As mentioned earlier, *NIX consists of small programs chained together to achieve the desired goal. Many programs in the OS are actually scripts, not binaries. This is possible due to the “do one thing right, expose a defined interface” paradigm and enables the administrator to customize the system to fit certain needs. This section of the chapter deals with the process of writing scripts. It presents a simple starting point, which evolves over time. The beauty of the *NIX approach is to start simple and go to sophisticated if needed. This approach enables the writer of the script to test the basic functionality, thus laying a solid foundation before extending the capabilities of the script. The script grows in manageable steps, allowing the writer to tackle the task at hand based on existing experience and knowledge.
