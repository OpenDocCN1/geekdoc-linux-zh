specifications in RAM and then the */usr/share/lib/terminfo* directory, which contains the terminal definition files. If the TERM variable is not set or is set incorrectly, the command results in no action.

# ## The echo Command

The `echo` command makes the terminal reiterate what you have just typed, as shown in Example 3.16. This procedure seems trivial when simply entered interactively on the screen, but the command can be valuable when included in shell scripts or similar files (for example, batch files). For instance, the `echo` command is helpful when you are writing a script file and you want to be notified when certain instructions are executing.

# **Example 3.17** *echo*

Freston spends the first couple of hours a day fighting user fires. After that, he tries to dedicate some time to automating some of his administration functions. Here, he practices with `echo` prior to using it in a configuration script:

```
$ echo Installing modem drivers now. . . <Enter>

Installing modem drivers now. . .
```

A few of the argument-like conventions that you can use with the `echo` command are \b to display a backspace character, \n to display a new-line (where the Enter key has been pressed) character, and \t to display a Tab character. See the online man pages or other information sources for an exhaustive list.

# ## The banner Command

The `banner` command displays ASCII character strings in large format on the screen or printed as hard copy. It constructs the characters out of # symbols and displays them from the top down (not from left to right). Like `echo`, this command might seem trivial when you play with it at your terminal, but it can prove invaluable in a large office or network environment when, for example, you want to identify individual print jobs from a shared printer. The syntax is as follows:

```
$ banner [-wl] ascii_text<Enter>
```