K Shell System UNIX introduced the Korn Shell (ksh), written by David Kohn. This shell extended many features of the original Bourne Shell and added many new features. Some features of the Bourne Again Shell, such as command aliases and command-line editing, are based on similar features from the Korn Shell.

POSIX  The POSIX (Portable Operating System Interface) family is being developed by PASC (IEEE's Portable Application Standards Committee, www.posix.org). A comprehensive FAQ on POSIX, including many links, appears at www.opengroup.org/austin/papers/posix_faq.html.

POSIX 1003.2 describes shell functionality. The Bourne Shell provides the features that match the requirements of this standard. Efforts are under way to make the Bourne Again Shell fully comply with the POSIX standard. In the meantime, if you invoke bash with the --posix option, the behavior of the Bourne Shell will closely match the POSIX requirements.

# SHELL BASICS

This section covers and using startup files, redirecting standard error, writing and executing shell scripts, separating and grouping commands, implementing job control, and manipulating the directory stack.

# chsh: changes your login shell

The person who sets up your account determines which shell you use when you first log in the system or when you open a terminal emulator window in a GUI environment. Under Ubuntu, bash is the default shell. You can run any shell you like once you are logged in. Enter the name of the shell you want to use (bash, tsh, or another shell) and press RETURN; the next prompt will be of the new shell. Give an exit command to return to the previous shell. Because shells you call in this manner are nested (one runs on top of the other), you will be able to log out from your original shell. When you have nested shells, keeping exit commands until you reach your original. You will then be able to log.

Use the chsh utility to change your login shell permanently. First give the command chsh. In response to the prompt, enter your password and the absolute pathname of the shell you want to use (/bin/bash,/bin/tsh, or the pathname of another shell). When you change your login shell in this manner using a terminal emulator (page 125) in a GUI, subsequent terminal windows will not reflect the change until you log out of the system and log back in. See page 457 for an example of how to use chsh.

# STARTUP FILES

When a shell starts, it runs startup files to initialize it. Which files the shell depends on whether it is a login shell, an interactive shell that is not a login shell (such as you by getting the command bash), or a noninteractive shell (one used to