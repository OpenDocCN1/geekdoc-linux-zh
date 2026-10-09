
GNOME also provides many graphical utilities you can use to customize and work with the desktop. It supports MIME types; thus, when you double-click an object, GNOME generally knows which tool to use to display the data represented by the object. In sum, GNOME is a powerful desktop manager that can make your job both easier and more fun.

## EXERCISES

- 1. a. What is Nautilus?
    b. List four things you can do with Nautilus.
    c. How do you use Nautilus to search for a file?
- 2. What is a terminal emulator? What does it allow you to do from a GUI that you would not be able to do without one?
- 3. How would you search the entire filesystem for a file named today.odt?
- 4. a. List two ways you can open a file using Nautilus.
    b. How does Nautilus “know” which program to use to open different types of files?
    c. What are the three common Nautilus control bars? Which kinds of tools do you find on each?
    d. Discuss the use of the Nautilus location bar in textual mode.

## Advanced Exercises

- 5. Assume you are using a mouse with nine pointer buttons defined. How would you reverse the effects of using the mouse wheel?
- 6. a. How would you use Nautilus to connect to the FTP server at ftp.ubuntu.com?
    b. Open the following folders: ubuntu, dists, and lucid. How would you copy the file named Contents-i386.gz to the desktop? What type of file is Contents-i386.gz?
    c. How would you open the Contents-i386.gz file on the desktop? How would you open the Contents-i386.gz file on the FTP server? Which file opens more quickly? Why? Which file can you modify?
- 7. Discuss the client/server environment set up by the X Window System. How does the X server work? List three X clients. Where is the client and where is the server when you log in on a local system? What is an advantage of this setup?
- 8. Run `xwininfo` from a terminal emulator window and answer these questions:
    a. What does `xwininfo` do?
    b. What does `xwininfo` give as the name of the window you clicked? Does that agree with the name in the window’s titlebar?
    c. What is the size of the window? In which units does `xwininfo` display this size? What is the depth of a window?
    d. How can you get `xwininfo` to display the same information without having to click the window?
- 9. Find and install `xeyes` (not `tuxeyes`). Write an `xeyes` command to display a window that is 600 pixels wide and 400 pixels tall, is located 200 pixels from the right edge of the screen and 300 pixels from the top of the screen, and contains orange eyes outlined in blue with red pupils. (*Hint*: Refer to the `xeyes` man page.)

# 9

# The Bourne Again Shell

This chapter picks up where Chapter 7 left off. Chapter 27 expands on this chapter, exploring control flow commands and more advanced aspects of programming the Bourne Again Shell (bash). The bash home page is at www.gnu.org/software/bash. The bash info page is a complete Bourne Again Shell reference.

The Bourne Again Shell is a command interpreter and high-level programming language. As a command interpreter, it processes commands you enter on the command line in response to a prompt. When you use the shell as a programming language, it processes commands stored in files called shell scripts. Like other languages, shells have variables and control flow commands (for example, for loops and if statements).

When you use a shell as a command interpreter, you can customize the environment you work in. You can make your prompt display the name of the working directory, create a function or an alias for cp that keeps it from overwriting certain kinds of files, take advantage of keyword variables to change aspects of how the shell works, and so on. You can also write shell scripts that do your bidding—anything from a one-line script that stores a long, complex command to a longer script that runs a set of reports, prints them, and mails you a reminder when the job is done. More complex shell scripts are themselves programs; they do not just run other programs. Chapter 27 has some examples of these types of scripts.

Most system shell scripts are written to run under **bash** (or **dash**; see below). If you will ever work in recovery mode—when you boot the system or perform system maintenance, administration, or repair work, for example—it is a good idea to become familiar with this shell.

This chapter expands on the interactive features of the shell described in Chapter 7, explains how to create and run simple shell scripts, discusses job control, introduces the basic aspects of shell programming, talks about history and aliases, and describes command-line expansion. Chapter 27 presents some more challenging shell programming problems.

## BACKGROUND

The Bourne Again Shell is based on the Bourne Shell (the early UNIX shell; this book refers to it as the *original Bourne Shell* to avoid confusion), which was written by Steve Bourne of AT&T's Bell Laboratories. Over the years the original Bourne Shell has been expanded but it remains the basic shell provided with many commercial versions of UNIX.

**sh Shell**

Because of its long and successful history, the original Bourne Shell has been used to write many of the shell scripts that help manage UNIX systems. Some of these scripts appear in Linux as Bourne Again Shell scripts. Although the Bourne Again Shell includes many expansions and features not found in the original Bourne Shell, **bash** maintains compatibility with the original Bourne Shell so you can run Bourne Shell scripts under **bash**. On UNIX systems the original Bourne Shell is named **sh**.

**dash Shell**

The **bash** executable file is about 800 kilobytes, has many features, and is well suited as a user login shell. The **dash** (Debian Almquist) shell is about 100 kilobytes, offers Bourne Shell compatibility for shell scripts (noninteractive use), and, because of its size, can load and execute shell scripts much more quickly than **bash**. Most system scripts are set up to run **sh**, which under Ubuntu is a symbolic link to **dash**. This setup allows the system to boot and run system shell scripts quickly.

On many Linux systems **sh** is a symbolic link to **bash**, ensuring scripts that require the presence of the Bourne Shell still run. When called as **sh**, **bash** does its best to emulate the original Bourne Shell.

**Korn Shell**

System V UNIX introduced the Korn Shell (ksh), written by David Korn. This shell extended many features of the original Bourne Shell and added many new features. Some features of the Bourne Again Shell, such as command aliases and command-line editing, are based on similar features from the Korn Shell.

**POSIX**

The POSIX (Portable Operating System Interface) family of related standards is being developed by PASC (IEEE's Portable Application Standards Committee, www.pasc.org). A comprehensive FAQ on POSIX, including many links, appears at www.opengroup.org/austin/papers/posix_faq.html.

POSIX standard 1003.2 describes shell functionality. The Bourne Again Shell provides the features that match the requirements of this standard. Efforts are under way to make the Bourne Again Shell fully comply with the POSIX standard. In the meantime, if you invoke **bash** with the **`--posix`** option, the behavior of the Bourne Again Shell will closely match the POSIX requirements.

# SHELL BASICS

This section covers writing and using startup files, redirecting standard error, writing and executing simple shell scripts, separating and grouping commands, implementing job control, and manipulating the directory stack.

### csh: changes your login shell

> **tip** The person who sets up your account determines which shell you use when you first log in on the system or when you open a terminal emulator window in a GUI environment. Under Ubuntu, **bash** is the default shell. You can run any shell you like once you are logged in. Enter the name of the shell you want to use (**bash**, **tcsh**, or another shell) and press RETURN; the next prompt will be that of the new shell. Give an **exit** command to return to the previous shell. Because shells you call in this manner are nested (one runs on top of the other), you will be able to log out only from your original shell. When you nested several shells, keep giving **exit** commands until you reach your original shell. You will then be able to log out.

Use the **chsh** utility to change your login shell permanently. First give the command **chsh**. In response to the prompts, enter your password and the absolute pathname of the shell you want to use (**/bin/bash**, **/bin/tcsh**, or the pathname of another shell). When you change your login shell in this manner using a terminal emulator (page 125) under a GUI, subsequent terminal emulator windows will not reflect the change until you log out of the system and log back in. See page 457 for an example of how to use chsh.

# STARTUP FILES

When a shell starts, it runs startup files to initialize itself. Which files the shell runs depends on whether it is a login shell, an interactive shell that is not a login shell (such as you get by giving the command **bash**), or a noninteractive shell (one used to
