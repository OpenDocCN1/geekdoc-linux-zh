long-duration command as a foreground process, you can execute a command as a background process. You can then continue with other work in the foreground.

To run a background process, you end the command with an ampersand (&). Once a process is running in the background, you can perform additional tasks by entering other commands at your workstation.

After you create a background process, the following takes place:

+   - The Process Identification Number (PID) is displayed. The operating system creates and assigns PIDs so that all processes currently running on the system can be tracked. (In the Korn and POSIX shells or the C shell, job numbers are assigned as well.)
+   - The prompt returns so that you can enter another command.
+   - In the C shell, a message is displayed when the background process is complete.

When you create a background process, note its PID number. The PID number helps you to monitor or terminate the process. See Section 6.4 for more information.

Because background processes increase the total amount of work the system is doing, they may also slow down the rest of the system. This may or may not be a problem, depending upon how much the system slows and the nature of the other work you or others do while background processes run.

Most processes direct their output to standard output, even when they run in the background. Unless redirected, standard output goes to your workstation. Because the output from a background process may interfere with your other work on the system, it is usually good practice to redirect the output of a background process to a file or to a printer. Then you can look at the output whenever you are ready. For more information about redirecting output, see the examples later in this chapter as well as Section 6.2.

The examples in the remainder of this chapter use a command that takes more than a few seconds to run:

```
$ find / -type f -print
```

This command displays the pathnames for all files on your system. You do not need to study the find command in order to complete this chapter – it is used here simply to demonstrate how to work with processes. However, if you want to learn more about the find command, see the find(1) reference page.

In the following example, the find command runs in the background (by entering an ampersand [&]) and redirects its output to a file named dir.paths (by using the right-angle bracket [>] operator):