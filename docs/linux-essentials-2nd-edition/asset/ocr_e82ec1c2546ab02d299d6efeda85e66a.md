# Redirecting Input and Output

/etc/group:audio:x18:mythtv,david,pulse
/etc/group:cdrom:x19:haldaemon,david
[...

In this example, you haven't gained anything compared to typing grep david /etc/*, but you might have in other cases. For instance, suppose a command is producing several error messages. You might redirect standard error to a file and search for strings that might be relevant, and so on, even as you attempt to run the command, or a modified version of it, once more.

This next example illustrates how standard error and output are separate. If you type grep david /etc/* as a normal user (perhaps substituting your own username for david), you're likely to see output as shown earlier, specifying the files in which your username appears; however, you are likely to see error messages, since you lack permission to read some of the files in /etc.

```
grep: /etc/security: Permission denied
grep: /etc/shadow: Permission denied
```

The information on the files in which david appears is shown via standard output, the errors are shown via standard error. If you're not interested in the errors, you can redirect them to /dev/null—a device file that serves as a crash for data that you want to discard:

```
$ grep /etc/* 2> /dev/null
```

Likewise, if you redirect output to a file but not redirect standard error, you'll see the error messages on your screen. However, the file you create (such as david-in-etc.txt from the earlier command) will not contain the error messages. You might want to try all of the different types of output redirecting by using grep david /etc/* (substituting your own username for david) to get a feel for how they work.

Most programs have options, on the command line or in configuration files, that affect the wording of their output. Check the program's page to learn about such options.

The only difference between redirecting standard output using the > operator and redirecting standard error is the number 2. This is because the number 2 represents standard error at the command line.

Certification Objective

# Using Pipes

Another type of redirected output is a command-line pipe or pipeline. In a pipe, the standard output from one program is redirected as the standard input to a second program. You create a pipe using a vertical bar (|) between the two commands; this key is usually above the Enter key and accessed with Shift. Pipelines can be useful when applied in various ways. For instance, you might pipe the lengthy output of a program through the less pager, which enables you to page up and down through the output. In this

Chapter 6 describes the Less pager.

![](bbox=[0.095, 0.965, 0.235, 0.985])