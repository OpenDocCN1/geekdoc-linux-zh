# Accessing the CLI via a Linux Console Terminal

In the early days of Linux, when you booted up your system, you would see a login prompt on your monitor and that’s all. As mentioned earlier, this is called the Linux console. It was the only place you could enter commands for the system.

Even though several virtual consoles are created at boot time, many Linux desktop distributions switch to a graphical environment after the boot sequence completes. This provides the user with a graphical login and desktop experience. For these systems, accessing a virtual console is done manually.

On most Linux distributions, you can access one of the Linux virtual consoles using a simple keystroke combination. Usually, you must hold down the Ctrl+Alt key combination and then press a function key (F1 through F7) for the virtual console you want to use. Function Key F2 produces virtual console 2, key F3 produces virtual console 3, key F4 produces virtual console 4, and so on.

> **NOTE**
> 
> Linux distributions typically use the Ctrl+Alt key combination with a function key to reach the graphical interface. Ubuntu and Rocky Linux both use F3. However, it is best to test and see where your distribution puts the graphical interface, especially on older distribution versions.

Text mode virtual consoles use the whole screen and start with the text login screen displayed. An example of a text login screen from a virtual console is shown in Figure 2.2.

Notice in Figure 2.2 the word tty3 at the end of the first text line. The 3 in tty3 indicates that it is virtual console 3 and was reached by pressing the Ctrl+Alt+F3 key sequence. tty stands for teletypewriter. Teletypewriter is an old term, indicating a machine used for sending messages.

> **NOTE**
> 
> Not all Linux distributions show the virtual console’s tty number at the log screen. If you are logged into a virtual console, you can enter the command tty and press Enter to see which virtual console you are currently using. Entering commands is covered in Chapter 3, “Basic Bash Shell Commands.”

You log into a console terminal by entering your user ID after the login: prompt and typing your password after the Password: prompt. If you have never logged in this way before, be aware that typing your password is a different experience than in a graphical environment. In a graphical environment, you may see dots or asterisks indicating the password characters as you type. However, at the virtual console, nothing is displayed when you type your password.