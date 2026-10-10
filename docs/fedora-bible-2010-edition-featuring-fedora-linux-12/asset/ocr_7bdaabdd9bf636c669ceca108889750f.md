By default, Ctrl+Alt+F1 switches to the first virtual terminal, which is the terminal used to boot Linux. Ctrl+Alt+F7 switches back to the terminal used to run the X Window System— your graphical display. In between, with F2-F6, you get virtual terminals. These are especially useful if your graphical display appears to be hung.

If you find the X Window System hung, switch to another virtual terminal. Log in and run the following command:

```
$ ps -e | grep X
```

You should see a response with the command Xorg, such as the following:

```
2613 tty7 00:00:01 Xorg
```

The tty7 tells you that X is running on the virtual terminal associated with Ctrl+Alt+F7.

Next, send a signal to this program using the program's process ID (2613 in this case) with the kill command.

> **CAUTION:** Don't run this command unless you really need it. This forces all your desktop programs to stop and any work you have not saved will likely be lost.

For example:

```
# kill -HUP 2613
```

You will need to log in as the root user to run this command on the Xorg process.

This command causes the X server to restart. You should see the screen change and a spinning arrow cursor will display until the desktop restarts. You will need to log in again. In addition, the restarting process may switch to another virtual terminal, such as tty8 (accessible via Ctrl+Alt+F8).

You can also use Ctrl+Alt+Backspace to stop the X server. But, if X is hung, this key sequence may not work.

# Switching terminals with the screen program

A handy program called screen creates a form of text-based windowing on your terminal. You can use screen to get more than one virtual terminal inside a plain old Linux shell terminal.

> **TIP:** Screen is especially handy when you log onto remote systems using commands such as ssh. You can use screen to help you run multiple commands at the same time on the remote system, or to check on the progress of long-running remote commands.

To start screen, use the screen command:

```
$ screen
```