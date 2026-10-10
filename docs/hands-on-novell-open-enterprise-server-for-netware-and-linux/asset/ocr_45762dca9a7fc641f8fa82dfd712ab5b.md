![](bbox=[0.1, 0.05, 0.48, 0.25])

Figure 13-8 The Edit an Existing Local User dialog box

# WORKING WITH THE BASH SHELL

In Chapter 12, you learned how to work with the KDE interface for a number of administrative and user-oriented tasks. Although Linux now has more graphical environments to make it user friendly, network administrators still need to be comfortable working from the command line. Linux system operation is controlled through text-based configuration files that can be modified directly from command-line utilities. GUI environments make it more convenient to access applications and change many of these configuration files, but certain configuration parameters and applications still need to be managed through text-based commands.

# Accessing the Command-Line Interface

When a user first logs in to Linux, the user is placed in his or her home directory and given a command shell or GUI environment, depending on the run level specified for the system (explained in "Managing Linux Applications" later in this chapter). Because most systems are set to use a graphical run level, you need to open a terminal window to work with the command shell. Linux is a multiprocess OS, so you can have several terminal windows open at once and switch to a virtual terminal via the graphical console or by pressing Ctrl+Alt followed by the function key you want to assign to the terminal session. Holding down Ctrl+Alt and pressing F7, for example, returns you to the graphical console. Each terminal window is identified by a number in its title bar. Using multiple virtual terminals can come in handy when you're working on different projects and want to switch between commands quickly. Table 13-2 lists several commands that you work with in the following activity.

Table 13-2 Common Linux commands

| Linux Command | Description |
| :--- | :--- |
| ls | View directory contents. |
| cat | Display the contents of a text file. |
| cd | Change directory. |
| pwd | Display the current directory path. |
| su | Switch user; can be used to switch to the root user for certain administrative tasks. |
| id | Display user and group identification information about the logged-in user. |
| who | List all regular users logged in to the system. |