# Part I: The Linux Command Line

# FIGURE 2.2

Linux virtual console login screen.

![](bbox=[0.17, 0.19, 0.88, 0.53])

> **NOTE**
> Keep in mind that, within the Linux virtual console, you do not have the ability to run any graphical programs.

After logging into a virtual console, you are taken to the Linux CLI, and you can switch to another virtual console without losing your current active session. You can switch between all the virtual consoles, with multiple active sessions running. This feature provides a great deal of flexibility while you work at the CLI.

Additional flexibility deals with the virtual console’s appearance. Even though it is a text mode console terminal, you can modify the text and background colors.

For example, it may be easier on your eyes to set the background of the terminal to white and the text to black. After you have logged in, you can accomplish this modification in a couple of ways. One way is to type in the command `setterm --inversescreen on` and press the Enter key. You can also turn it off using the `off` option.

Another way is to type two commands, one after the other. Type `setterm --background white` and press Enter, and then type `setterm --foreground black` and press Enter. Be careful because when you change your terminal background first, it may be hard to see the commands you are typing.