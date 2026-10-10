other environments. You can also use text-based shells through text-mode network connections. Once you've started a shell, you can view and manipulate files and launch programs.

# # Starting a Shell

Linux supports many different shells, although precisely which ones might be installed varies from one distribution to another. The vast majority of Linux systems include Bash, which is usually the default shell for new users. Another common shell is known as *tcsh*, and many others, such as *zsh*, *csh*, and *ash*, are also available. Most shells are similar in broad strokes, but some details differ.

You can start a shell in many different ways, most of which are at least partially automatic. The following are the most common methods:

+   * **Logging in at the text-mode console** If you log into the computer using a text-mode console, you'll be greeted by your default shell, as it is set in your user account information (see Chapter 5, “Managing Users”).
+   * **Logging in remotely** Logging in remotely via Telnet, the Secure Shell (SSH), or some other remote text-mode login tool will start a shell. (Despite its name, SSH is not a shell in the sense described here, but it will start one automatically.)
+   * **Starting an *xterm*** An *xterm* is a GUI program in which text-based programs can run. By default, an *xterm* usually starts your default shell unless told to do otherwise.
+   * **Explicitly launching a shell** You can start one shell from within another. This can be helpful if you find you need features of one shell but are running another. Type the new shell's name to start it.

When you start a shell, you'll see a *Command prompt*. This is one or more characters that indicate the shell is waiting for input. *Command prompts* often (but not always) include your username, the computer's hostname, or the directory in which the shell is operating. For instance, a command prompt might resemble the following:

```
```bash
[rodsmi th@nessus /mnt]$ 
```
```

Although not a universal convention (it can be set in a user's shell configuration files), the final character is often a dollar sign ($) or greater-than symbol (>) for ordinary users or a hash mark (#) for *root*. This serves as an indication of *superuser* status; you should be cautious when entering commands in a root shell, because it's easy to damage the system from such a shell.

![](bbox=[0.14, 0.83, 0.24, 0.87])

This book includes command examples on separate lines. When the command is one that an ordinary user might issue, it's preceded by a $ prompt; when only *root* should be issuing the command, it's preceded by a # prompt. Because the username, computer name, and directory are usually unimportant, this information is omitted from the prompts printed in this book. The prompts are omitted from command examples within a paragraph of text.