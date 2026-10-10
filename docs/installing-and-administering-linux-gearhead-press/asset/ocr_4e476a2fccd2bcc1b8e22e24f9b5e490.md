![](bbox=[0.12, 0.08, 0.88, 0.48])

**Figure 12.2** Invoking a new shell and stopping the original shell.

that shell would have a new *PID*. Here, you will notice that when a new shell is invoked that is different from the login shell, the user prompt has changed (see Figure 12.2).

As it is invoked, the new shell will read its own environment files, which are usually different from the previous shell’s files. You can tell that a new shell has been invoked just by looking at the screen. This time, though, when you enter the *ps* command, the new shell will naturally have a different name from the previous shell but will have inherited the previous shell’s *PID*.

# **Example 12.3 The *ps -auxf* Command to Examine Parent-Child Processes**

To illustrate some parent-child process relationships, suppose that Lady Toloso logs into her terminal and types the following command and options at the command line: