execute the commands in it. Fedora/RHEL puts appropriate commands in some of these files. This section covers **bash** startup files.

# Login Shells

A **login shell** is the first shell that displays a prompt when you log in on a system from the system console or a virtual console (page 121), remotely using **ssh** or another program (page 121), or by another means. When you are running a GUI and open a terminal emulator such as **gnome-terminal** (page 120), you are not logging in on the system (you do not provide your username and password), so the shell the emulator displays is (usually) not a login shell; it is an interactive nonlogin shell (below). Login shells are, by their nature, interactive. See “**bash** versus **–bash**” on page 1023 for a way to tell which type of shell you are running.

This section describes the startup files that are executed by login shells and shells that you start with the **bash** **––login** option.

The shell first executes the commands in /etc/profile, establishing systemwide default characteristics for users running **bash**. In addition to executing the commands it holds, **profile** executes the commands within each of the files with a .sh filename extension in the /etc/profile.d directory. This setup allows a user working with **root** privileges to modify the commands **profile** runs without changing the **profile** file itself. Because **profile** can be replaced when the system is updated, making changes to files in the **profile.d** directory ensures the changes will remain when the system is updated.

# Set environment variables for all users in /etc/profile or in a *.sh file in /etc/profile.d

> Setting and exporting a variable in /etc/profile or in a file with a .sh filename extension in the /etc/profile.d directory makes that variable available to every user's login shell. Variables that are exported (placed in the environment) are also available to all interactive and noninteractive subshells of the login shell.

Next the shell looks for ~/.bash_profile, ~/.bash_login, or ~/.profile (~ is shorthand for your home directory), in that order, executing the commands in the first of these files it finds. You can put commands in one of these files to override the defaults set in /etc/profile.

By default, Fedora/RHEL sets up new accounts with ~/.bash_profile and ~/.bashrc files. The default ~/.bash_profile file calls ~/.bashrc, which calls /etc/bashrc.

When you log out, **bash** executes commands in the ~/.bash_logout file. This file often holds commands that clean up after a session, such as those that remove temporary files.

# Interactive Nonlogin Shells

The commands in the preceding startup files are not executed by interactive, nonlogin shells. However, these shells inherit from the login shell variables that are declared and exported in these startup files.