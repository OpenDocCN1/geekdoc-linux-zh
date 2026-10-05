
menubar: File->Open. Another row of tabs appears below the menubar as gnome-terminal opens on top of the existing one. Add as many terminal sessions as you like; click the tabs to switch between sessions.

# GNOME terminal emulator shortcuts

**tip:** While using the GNOME terminal emulator, CONTROL-SHIFT-N opens a new window and CONTROL-SHIFT-T opens a new tab. New windows and tabs open to the working directory. In addition, you can use CONTROL-PAGE UP and CONTROL-PAGE DOWN to switch between tabs.

A session you add from the context menu uses the same profile as the session you open it. When you use the menubar to open a session, GNOME gives you a choice of profiles, if more than one is available. You can add and modify profiles, including the Default profile, by selecting Terminal emulator: Edit->Profiles. Highlight the profile you want to modify or click New to design a new profile.

## ## Chapter Summary

The window managers, and virtually all X applications, are designed to help users tailor their work environments in simple or complex ways. You can designate applications that start automatically, set such attributes as colors and fonts, and even alter the way keyboard strokes and mouse clicks are interpreted.

Built on top of the X Window System, the GNOME desktop manager can be used as is or customized to better suit your needs. It is a graphical interface to system services (the filesystem, applications, and more). Although not part of GNOME, the Metacity and Compiz window managers work closely with GNOME and are the default window managers for GNOME under Ubuntu. A window-manager controls all aspects of the windows, including placement, decoration, grouping, minimizing and sizing, and moving.

The Nautilus File Browser window is a critical part of GNOME; the desktop is a modified File Browser window. The File Browser pane displays icons or a list of filenames you can work with. The Side pane, which can display six types of information, augments the information Nautilus displays in the View pane.

GNOME also provides many graphical utilities you can use to customize and work with the desktop. It supports MIME types; thus, when you double-click an object, GNOME generally knows which tool to use to display the data represented by the object. In sum, GNOME is a powerful desktop manager that can make your job easier and more fun.

# EXERCISES

- 1. a. What is Nautilus?
  b. List four things you can do with Nautilus.
  c. How do you use Nautilus to search for a file?
- 2. What is a terminal emulator? What does it allow you to do from a GUI that you would not be able to do without one?
- 3. How would you search the entire filesystem for a file named today?
- 4. List two ways you can open a file using Nautilus.
  b. How does Nautilus “know” which program to use to open different types of files?
  c. What are the three common Nautilus control bars? Which kinds of tools do you find on each?
  d. Discuss the use of the Nautilus location bar in textual mode.

# ADVANCED EXERCISES

- 5. Assume you are using a mouse with nine pointer buttons defined. How would you reverse the effects of using the mouse wheel?
- 6. How would you use Nautilus to connect to the FTP server at ftp.ubuntu.com?
- 7. Open the following folders: ubuntu, dists, and lucid. How would you copy the file name Contents-i386.gz to the desktop? What type of file is Contents-i386.gz?
- 8. How would you open the Contents-i386.gz file on the desktop? How would you open the Contents-i386.gz file on the FTP server? Which file opens more quickly? Why? Which file can you modify?
- 9. Discuss the client/server environment set up by the X Window System. How does the X server work? List three X clients. Where is the client and where is the server when you log in on a local system? What is an advantage of this setup?
- 8. Run xwininfo from a terminal emulator window and answer these questions:
  a. What does xwininfo do?
  b. What does xwininfo give as the name of the window you clicked? Does that agree with the name in the window's titlebar?
  c. What is the size of the window? In what units does xwininfo display this size? What is the depth of a window?
  d. How can you get xwininfo to display the same information without having to?
- 9. If you will ever work in recovery mode—when you boot the system or perform system maintenance, for example—it is a good idea to become familiar with this shell.

# THE BOURNE AGAIN SHELL

## IN THIS CHAPTER

- Startup ...... 293
- Redirecting Standard ...... 297
- Writing Simple Script ...... 300
- Job Control ...... 307
- Manipulating Directory ...... 310
- Parameters and Variables ...... 312
- History ...... 330
- Editing ...... 332
- Functions ...... 349
- Features and Options ...... 352
- Processing Command Line ...... 356

This chapter expands on the interactive features of the shell described in Chapter 7, explains how to create and run simple scripts, discusses job control, introduces the basic aspects of shell programming, talks about history and aliases, and describes command expansion. Chapter 27 presents some more challenging shell programming problems.

# BACKGROUND

The Bourne Again Shell is based on the Bourne Shell (the early UNIX shell; this book refers to it as the original Bourne Shell to avoid confusion), which was written by Steve Bourne of AT&T's Bell Laboratories. Over the years the original Bourne Shell has been expanded but it remains the basic shell provided with many commercial versions of UNIX.

sh Shell Because of its long and successful history, the original Bourne Shell has been used to write many of the shell scripts that manage UNIX systems. Some of these scripts appear in Linux as Bourne Shell scripts. Although the Bourne Again Shell includes many extensions and features not found in the original Bourne Shell, bash maintains compatibility with the original Bourne Shell so you can run Bourne Shell scripts under bash. On UNIX systems the original Bourne Shell is named sh.

dash Shell The bash executable is about 800 kilobytes, has many features, and is well suited as a user login shell. The dash (Debian Minimal) is about 100 kilobytes, offers Bourne Shell compatibility for shell scripts (noninteractive use), and because of its size, can load and execute shell scripts much more quickly than bash. Most system scripts are set up to run sh, which Ubuntu is a symbolic link to dash. This setup allows the system to boot and run system shell scripts quickly.

On many Linux systems sh is a symbolic link to bash, ensuring scripts require the presence of the Bourne Shell still run. When called as sh, bash does its best to emulate the original Bourne Shell.
