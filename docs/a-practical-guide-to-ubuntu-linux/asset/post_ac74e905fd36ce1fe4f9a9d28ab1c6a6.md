
to perform administrative tasks. After you enter your password, the program runs with root privileges. Second, if you use the sudo utility (for textual applications; page 421) or gksudo utility (for graphical applications; page 423) from the command line (like from a terminal emulator; page 125) and provide your password, the command you enter runs with root privileges. In both cases you cease with root privileges when the command finishes or when you exit the program with root privileges. For more information refer to “Running Commands with Root Privileges” on page 419.

## Do not experiment while you are working with root privileges

**Caution**: Feel to experiment when you are not working with root privileges. When you are working with root privileges, only what you have to do and make sure you know exactly what you are doing. After you have completed the task at hand, revert to working as yourself. When working with root privileges, you can damage the system to such an extent that you will need to reinstall Linux to get it working again.

## A TOUR OF THE UBUNTU DESKTOP

This section presents new words (for some readers) in a context that explains the terms well enough to get you started with the Linux desktop. If you would like exact definitions as you read this section, refer to “GNOME Desktop Terminology” on page 117 and to the Glossary. The Glossary also describes the data entry widgets (page 1180), such as the combo box (page 1141), drop-down list (page 1146), list box (page 1157), and text box (page 1176).

GNOME (www.gnome.org), a product of the GNU project (page 5), is the user-friendly desktop manager under Ubuntu. KDE, the K Environment, is a powerful desktop manager and complete set of tools you can use in place of GNOME (www.kde.org/community/whatkde). The version of Ubuntu that is named Ubuntu.

This tour describes GNOME, a full-featured, mature desktop environment that boasts a rich assortment of configurable tools. This section covers desktop features—including panels, objects, and workspaces—and explains how to easily move from one workspace to another. It describes several ways to launch objects (run programs) from the desktop, how to set up the desktop to meet your needs and please your senses, and how to manipulate windows. As the tour continues, it explains how to work with files and folders using the Nautilus File Browser window, one of the most important GNOME tools. The tour concludes with a discussion of the Update Manager, that allows you to keep a system up-to-date with the click of a button; getting help; and logging out.

## LOGGING IN ON THE SYSTEM

When you boot a standard Ubuntu system, GDM (GNOME display manager) displays a Login screen (Figure 4-1) on the system console. In the middle of the screen is a window that holds a list of names. When you click a name, Ubuntu displays a text box labeled Password. In addition, in the panel at the bottom of the screen, Ubuntu displays icons that allow you to work in a different language, select a different keyboard layout, change your accessibility preferences (e.g., make the text larger and easier to read), and restart or shut down the system. For more information refer to "The Login Screen" on page 145.

To log in, click your name. A text box labeled Password appears. Enter your password and press RETURN. If Ubuntu displays an error message, clicking your name and entering your password again. Make sure the CAPS LOCK is not on (Ubuntu displays a message if it is) because the routine that verifies your entries is case sensitive. See page 146 if you need help with logging and page 148 if you want to change your password. The system takes a moment to set things up and then displays a workspace (Figure 4-2).

## INTRODUCTION

You can use the desktop as is or you can customize it until it works and functions nothing like the initial desktop. If you have a computer of your own, you may want to add a user (page 594) and work as that user you experiment with the desktop. When you figure out which features you like, you can log in as yourself and implement these features. That way you need not concern yourself with "ruining" your desktop and not being able to get it back to a satisfactory configuration.

![](img/45ff4cd21497435daa35084a84b95d07_150_0.png)

Figure 4-1 The Ubuntu GNOME Login screen

![](img/45ff4cd21497435daa35084a84b95d07_151_0.png)

## Figure 4-2 The initial workspace

When you log in, GNOME displays a workspace that includes Top and Bottom panels (bars) that are essential to getting your work done easily and efficiently (Figure 4-2). Each of the panels holds several icons and words objects (Buttons, applets, and menus, for example, are all types of objects). When you click an object, something happens.

A panel does not allow you to do anything you could not otherwise, but rather collects objects in one place and makes your work with the system easier. Because the panels are easy to configure, you can set them up to hold those tools you use freely. You can create additional panels to hold different groups of tools.

What you displayed on the screen is a workspace. Initially Ubuntu configures GNOME with four workspaces. The desktop, which is not displayed at all once, is the collection of all workspaces. “Switching Workspaces” on page 114 describes some of.

## Do not experiment while you are working with root privileges

**Caution**: Feel to experiment when you are not working with root privileges. When you are working with root privileges, only what you have to do and make sure you know exactly what you are doing. After you have completed the task at hand, revert to working as yourself. When working with root privileges, you can damage the system to such an extent that you will need to reinstall Linux to get it working again.

## LAUNCHING PROGRAMS FROM THE DESKTOP

You can run command-line utilities, which are textual (not graphical), from the Applications window. When you run a textual utility from this window, you must put a tick in the check box labeled Run in terminal (click the box to put a tick in it; click again to remove it). The ticks tell GNOME to run the command in a terminal window. When the utility finishes running, GNOME closes the window.

For example, type vim.tiny (the name of a text-based editor) in the text box, put a tick in the check box labeled Run in terminal, and click Run. GNOME opens a Terminal (emulator) window and runs the vim text editor. When you exit by vim (press ESCAPERETURN to do so), GNOME closes the Terminal.

You can also start a program by pressing Alt-F to display the Run Application window (Figure 4-4). As you start to type firefox in the text box, the window recognizes that you are typing and displays the Firefox logo. Click Run to start.

You can run a command-line utility that only displays output and terminates. Because the window closes as soon as the utility is finished running, and most utilities run quickly, you will probably not see the output. Type the following command to run the df h (disk free; page 774) utility and keep the window open until you press RETURN (remember to put a tick in the check box labeled Run in terminal):

```
bash -c "df -h; read"
```

This command starts a bash shell (Chapter 7) that executes the command line following the -c option. The command line holds two commands separated by a semicolon. The second command, read (page 1003), waits for you to press RETURN before terminating. Thus the output from the df command remains on the screen until you press RETURN. Replace read with sleep 10 to have the window remain open for ten seconds.
