Korn Shell System V UNIX introduced the Korn Shell (ksh), written by David Korn. This shell extended many features of the original Bourne Shell and added many new features. Some features of the Bourne Agai n Shell, such as command aliases and command-line editing, are based on similar features from the Korn Shell.

POSIX The POSIX (Portable Operating System Interface) family of related standards is being developed by PASC (IEEE's Portable Application Standards Committee, www.pasc.org). A comprehensive FAQ on POSIX, including many links, appears at www.opengroup.org/austin/papers/posix_faq.html.

POSIX standard 1003.2 describes shell functionality. The Bourne Agai n Shell provides the features that match the requirements of this standard. Efforts are under way to make the Bourne Agai n Shell fully comply with the POSIX standard. In the meantime, if you invoke **bash** with the **`--posix`** option, the behavior of the Bourne Agai n Shell will closely match the POSIX requirements.

# # SHELL BASICS

This section covers writing and using startup files, redirecting standard error, writing and executing simple shell scripts, separating and grouping commands, implementing job control, and manipulating the directory stack.

# ## csh: changes your login shell

> tip The person who sets up your account determines which shell you use when you first log in on the system or when you open a terminal emulator window in a GUI environment. Under Ubuntu, **bash** is the default shell. You can run any shell you like once you are logged in. Enter the name of the shell you want to use (**bash**, **tcsh**, or another shell) and press RETURN; the next prompt will be that of the new shell. Give an **exit** command to return to the previous shell. Because shells you call in this manner are nested (one runs on top of the other), you will be able to log out only from your original shell. When you nested several shells, keep giving **exit** commands until you reach your original shell. You will then be able to log out.

Use the **chsh** utility to change your login shell permanently. First give the command **chsh**. In response to the prompts, enter your password and the absolute pathname of the shell you want to use (**/bin/bash**, **/bin/tcsh**, or the pathname of another shell). When you change your login shell in this manner using a terminal emulator (page 125) under a GUI, subsequent terminal emulator windows will not reflect the change until you log out of the system and log back in. See page 457 for an example of how to use chsh.

# # STARTUP FILES

When a shell starts, it runs startup files to initialize itself. Which files the shell runs depends on whether it is a login shell, an interactive shell that is not a login shell (such as you get by giving the command **bash**), or a noninteractive shell (one used to