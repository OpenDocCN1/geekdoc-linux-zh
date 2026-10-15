![](bbox=[0.18, 0.12, 0.56, 0.55])

# Figure 9.1 Starting the C shell.

which is an initialization file that allows you to customize the C/TC shell environment in which you will be working. After executing commands in the .cshrc or .tcshrc file, commands in the .login file are executed. The .cshrc or .tcshrc file will be executed every time a new C/TC shell is started. The .login file is executed only once when the user logs on, and also contains commands and variables to initialize the user's environment. After executing commands from those files, the prompt appears on your screen and the C/TC shell awaits commands. Most systems today start up with a graphical user interface, adding to the steps just mentioned. When you are in the desktop, such as CDE, you will see icons and menus. Once you select a terminal from the menu, the shell prompt will appear and you can start typing commands.

# 9.2 The Environment

# 9.2.1 Initialization Files

After the csh/tcsh program starts, it is programmed to execute two files in the user's home directory: the .cshrc or .tcshrc file, respectively, and the .login file. These files allow users to initialize their own environments.