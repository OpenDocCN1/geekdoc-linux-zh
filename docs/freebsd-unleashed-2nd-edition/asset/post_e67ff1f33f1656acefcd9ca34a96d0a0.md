
## Using Alternate Shells

Any user can change his or her assigned shell at any time. The reasons for doing this are myriad: The user might be accustomed to Linux and bash, as described earlier, or have a highly customized shell environment from another system that is only in a certain shell’s configuration format (as we’ll discuss shortly). Regardless of the reason, changing a user’s shell is pretty easy.

### Changing Your Shell While Logged In

The simplest way to use an alternate shell is simply to run it. If your default shell is csh, and you want to use bash (assuming that bash is available on the system), just type `bash` to open a new bash environment within your csh session, as shown here:

```
# bash
bash-2.04#
```

Now, when you log out, you’ll have to do it twice—once to exit the bash process and again to exit the original csh process. When your login shell program exits, you are disconnected from the system.

### Changing Your Default Shell

Running a shell other than your default one every time you log in can get tedious. Although you can do it automatically by adding the command for the second shell into your `.login` file (an initialization script that runs when the shell is started, as we’ll learn in “csh/csh Files: .cshrc, .login, and .logout,” later in this chapter), this still means you’re running a shell within a shell, which isn’t very efficient. Fortunately, any user can change his or her shell to any program listed in `/etc/shells`. The `chsh` (change shell) program is used for this task. This program differs in its behavior from platform to platform. On some platforms, such as Linux, `chsh` is a command-line, interactive tool that prompts for new values one by one. In FreeBSD, however, `chsh` is really the same program as `chpass`, `chfn`, and other user-management tools. They’re all hard links to each other, and they all have the same function.

The behavior of `chsh` (and its identical siblings) is to open your user information in a text editor and allow you to change the values in any of the available fields. The editor used by default is `vi`, although this can be overridden by setting the `EDITOR` environment variable to the name of a different program, such as `ee` or `pico`. (We’ll talk about environment variables in the upcoming section “Shell Initialization Files.”)

To change your own shell, simply enter `chsh`. If you’re root, you can modify another user’s shell by supplying that user’s login as the argument. Here’s an example:

```
# chsh frank
# Changing user database information for frank.
Shell: /bin/tcsh
Full Name: Frank Allen
Office Location:
Office Phone:
Home Phone:
Other information:
```

A full discussion of how to use the `vi` editor is found in Chapter 6, “Working with Applications.” For now, let’s concentrate on the necessary commands you’ll need for changing the user’s shell.

Part of what makes `vi` so challenging is that its internal commands are so arcane and must be entered so exactly that it’s easy to get to a point at which crucial data has been accidentally deleted or mangled and can’t be retrieved. If you make a mistake, enter a colon (`:`), followed by `q!`, and then press Enter, which will force an exit without saving changes:

```
:
:q!
```

Let’s say you want to change frank’s shell permanently from `/bin/tcsh` to `/usr/local/bin/bash`. Once you’re in the `vi` screen, obtained by typing `chsh frank`, use the arrow keys to move to the beginning of the word `tcsh`, immediately after the second slash (`/`). Type `c` (for “change”) and then `w` (for “word”). A dollar sign (`$`) will appear at the end of the word you’re changing:

```
Shell: /bin/tcsh$
```

Type `bash` in place of the word `tcsh` and then press Esc to exit change-word mode. Now the shell is `/bin/bash`. The next step is to place the cursor on top of the first slash, just before `bin`, and type `i` (for “insert”) to get a usable cursor. Enter `/usr/local` and then press Escape. The shell string should now be `/usr/local/bin/bash`.

Now, enter a colon (`:`) to go into the in-program command line and then follow it with `w` (for “write”). Press Enter to save the file. Finally, type `:q` and press Enter to quit.

The file you’ve now written is actually a temporary file in `/etc`. If your changes are valid, they will be read from that file and automatically rebuilt into `/etc/master.passwd` and `/etc/passwd`. From now on, every time the user in question logs in to the system, the login will be under `/usr/local/bin/bash` rather than `/bin/tcsh`.

If the changes you've made are not valid (for example, if the shell you specified is not listed in `/etc/shells`), you are given the choice to re-edit the user profile or to cancel the operation.

### Non-Shell Programs as Shells

It's possible to set a user's shell to a program that isn't specifically designed to be a shell; programs such as `/sbin/nologin`, for example, do nothing but print out a text banner and exit. Also the user might prefer to use some programs tailored to command-line interaction with services other than the Unix filesystem (such as TinyFuge).

You can set a nonexistent program as a user's shell to prevent the user from logging in at all. You can even set a user's shell to `/usr/bin/mail` (the shell-based mail reader) if you want, although this will mean that the user can't do much but read mail. On the other hand, this might be the server policy you decide to set.

The `chsh` program will warn you if you specify a shell that doesn't exist, but it will still dutifully write it into the user database. There's nothing wrong with having a user's shell set to a nonexistent program; it simply means that the user won't be able to log in. Remember, a login shell works as follows:

- If the program can be successfully executed and attached to a pty (pseudo-terminal), the login will be successful and will not end until the shell program terminates and releases the pty.
- If the shell program can't be executed, nothing will bind to the pty, and the user won't get a command line. Instead, the user gets an error. Depending on the terminal program, the error might take the shape of a password-authentication error or a protocol failure error. In a command-line telnet session, the error might result in an explicit failure to execute the shell program after displaying the various login banners, as shown here:

```
FreeBSD/i386 (stripes.somewhere.com) (ttyu2)

login: frank
Password:
Last login: Sat May  5 18:35:52 from w044.z064002043.
Copyright (c) 1980, 1983, 1986, 1988, 1990, 1991, 1993, 1994
    The Regents of the University of California.  All rights reserved.

FreeBSD 4.6.2-RELEASE (STRIPES) #0: Wed Aug 14 20:47:38 PDT 2002
------------------------------------------------------------
Welcome to the system! Today's news: nothing.

You have mail.
login: /usr/local/bin/foosh: No such file or directory
Connection closed by foreign host.
```

You can leverage this behavior of displaying the general login banners before executing a user's shell. For instance, if you have a troublesome user or group of users who have violated system policy in some way (such as by hacking), you can prevent them from logging in by setting their shells to a nonexistent program and giving an explanation of a systemwide policy enforcement change in `/etc/motd`. This “message of the day” file is a regular text file that the system displays as a banner to every user immediately after accepting his or her password. Edit `/etc/motd` in your favorite text editor to reflect anything you want all your users, including ones without valid shells, to read upon login.

An even more useful (and correct) method is to set the user's shell to a program that isn't really a shell but merely a program that prints out informative text. `/sbin/nologin` is a built-in program that you can set as a user's shell to disable his or her login. This shell script prints out a single line of text and then exits. The line of text is short and sweet:

```
This account is currently not available.
```

Notice that `/sbin/nologin` executed, attached to the pty, exited properly, and released the pty. The fact that it never presented any kind of interactive command line doesn't make it any less valid as a shell. This method of disabling an account works for any terminal program, whether using `telnet` or `ssh`, and it involves no errors or warnings. It's very elegant and extensible.

You can, in fact, assign any program as the shell, regardless of whether the program is interactive. You can make your shell `/bin/ls` or `/usr/bin/finger`, if you like. More usefully, you can create your own script or program to execute when a certain user logs in. This way, you can set up interesting services on your system, such as a customized “library” system in which guests can log in and interact with a menu, execute a certain limited set of commands, or simply get a screenful of information. The possibilities are endless!

> **CAUTION**
>
> A word of warning is in order: If you write a login handler for the purpose of providing custom services in C or another language in which you have to allocate your own buffer space, beware of potential buffer overflows! These are the most common types of security holes found in network services; if an attacker is able to find and exploit a buffer overflow in a program you devise yourself, and there is any way for the program to run executable code as root (for example, if it's a setuid program owned by root), your system belongs to that attacker. Be very careful in this area!
