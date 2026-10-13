If, for some reason, the GUI seems to be *hung* (you click and type, but nothing happens), you can turn to the **virtual consoles**. (The *physical* console is the monitor-and-keyboard combination.) The idea of virtual consoles is to give you the ability to switch between several text consoles, even though you can have only one physical console. Whether you are running a GUI or not, you can then use different text consoles to type different commands.

To get to the first virtual console from the GNOME or KDE desktop, press Ctrl+Alt+F1. Press Ctrl+Alt+F2 for the second virtual console, and so on. Each of these virtual consoles is a text screen where you can log in and type Linux commands to perform various tasks. When you’re done, type **exit** to log out.

You can use up to six virtual consoles. In most distributions, the seventh one is used for the GUI desktop. To get back to the GUI desktop, press Ctrl+Alt+F7.

If the GUI appears to be hung, switch to a virtual console and gracefully shut down the system from that console. For example, press Ctrl+Alt+F2 and then log in as root. After that, type **shutdown -h now** to halt the system. To restart the system, type **reboot**.

![](bbox=[0.12, 0.32, 0.21, 0.39])

![](bbox=[0.12, 0.4, 0.21, 0.47])

# Exploring the Bash Shell

If you’ve used MS-DOS, you may be familiar with COMMAND.COM, the DOS command interpreter. That program displays the infamous C:\> prompt. In Windows, you can see this prompt if you open a command window. (To open a command window in Microsoft Windows, choose Start➜Run, type **cmd** in the text box, and then click OK.)

SUSE Linux comes with a command interpreter that resembles COMMAND.COM in DOS, but it can do a whole lot more. The SUSE Linux command interpreter is called a *shell*.

The default shell in SUSE Linux is **bash**. When you open a terminal window or log in at a text console, the bash shell is what prompts you for commands. Then, when you type a command, the shell executes your command.

In addition to the standard Linux commands, bash can execute any computer program. So you can type the name of an application (the name is usually more cryptic than what you see in GNOME or KDE menus) at the shell prompt, and the shell starts that application.