# Managing Shared Libraries

SysV startup scripts, but these scripts weren't always transportable across distributions. Today, alternatives to SysV are common, which further complicates the problem. The result is that the server you installed may not start up. Possible workarounds include modifying the startup script that the server, building a new script based on another from your distribution, and starting the server through a local startup script /etc/rc.d/.local or /etc/rc.d/.boot.local. Chapter 5, "Booting Linux and Editing Files,"
describes startup scripts in more detail.

> NOTE Startup script problems affect only servers and other programs that are started automatically when the computer boots; they don't typical user applications or libraries.

# Managing Shared Libraries

Most Linux relies heavily on shared libraries. The preceding sections have described some of the problems that can arise in managing shared library packages—for example, if a library is not installed or is the wrong version, you may have problems installing a package. Library management goes beyond merely configuring them, though. To understand this, you must first understand a few library principles. You can then move on to setting the library path and using commands that manage libraries.

# Library Principles

The idea behind a library is to simplify programmers' lives by providing common programs. For instance, one of the most important libraries is the C library (libc), which provides many of the higher-level features associated with the C programming language. Another common type of library is associated with GUIs. These libraries are often called widget sets because they provide the on-screen widgets—buttons, scroll bars, menu bars, and so on. The GIMP Tool Kit (GTK+) and Qt are the most popular Library sets, and both ship largely as libraries. Libraries are chosen by programmers, not by users; you usually can't substitute one library for another. (The main exceptions are minor upgrades).

> NOTE Linux uses the GNU C library (glibc) version of the C library. Package-manager dependencies and other library references refer to glibc specifications. As of glibc 2.15, for historical reasons the main glibc file is usually called /lib/libc.so.6 or /lib64/libc.so.6, but this file is sometimes a symbolic link to a file of another name, such as /lib/libc-2.15.so.