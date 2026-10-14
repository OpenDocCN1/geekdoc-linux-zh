
working directory. To see a list of all the environment variables currently defined, type set at the prompt.

When you type a command at the shell prompt, the shell will look for that command’s program file in each directory listed in the PATH variable, in order. The first program found matching the command you typed will be run. If the command’s program file is not in a directory listed in your PATH environment variable, the shell returns a "command not found" error.

By default, the shell does not look in your current working directory or your home directory for commands. This is really a security mechanism so that you don’t execute programs by accident. What if a malicious user put a harmful program called ls in your home directory? If you typed ls and the shell looked for the fake program in your home directory before the real program in the /bin directory, what do you think would happen? If you thought bad things, you are on the right track.

Since your PATH doesn’t have the current directory (.) as one of its search places, programs in your current directory must be called with an absolute path or a relative path specified as ./programname.

To see what directories are part of your PATH, enter this command:

```
echo $PATH
```

```
[alberto@digital alberto]$ echo $PATH
/bin:/usr/bin:/opt/bin:/usr/local/bin:/usr/X11R6/bin:/opt/kde/bin:
```

Note that directory paths are separated by a colon (:).

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Filename Expansion: Tab

As I said earlier, shells are not very ergonomic, and most people don’t like to type commands or long pathnames very often. Depending on the shell of you use, you might have the ability to have the shell complete filenames and command names for you. The shell will do this whenever the portions of the path you specified cannot be confused for something else.

To activate completion on bash, all you need to do is press Tab after you’ve typed enough characters. If you wanted a listing of the /usr/local/bin directory, you could type ls /u<Tab>/lo<Tab>/b<Tab>, and the shell will expand each of the paths for you, saving you some keystrokes.

If the shell cannot complete the expansion because multiple completions are possible, hitting Tab again will list everything that could be a match. This is very useful if you have forgotten the name of a command. For example if you type l<Tab><Tab>, the shell will respond with a list of all the programs that begin with an l:

```
[alberto@digital alberto]$ l<Tab><Tab>
laser        lesskey      lkbib        lockfile     lpr
last         let          lmorph       logger       lprm
lastb        lex          ln           login        lptest
lastcomm     lha          lnd ir       logname      ls
latex        lightning    loadkeys     logout       lsattr
lbxproxy     lintopvf     loadunimap   look         lsdev
ld           lisa         local        lookbib      lynx
ld86         lispm tpgm   locale       lout         lz
ldd          listalias    localedef    lpq
less         listres      locate       lpqall.faces
```

## Exiting the Console

To exit a console, issue the logout command. This command will end your session, clear up the screen, and return you to the login prompt. To restart the computer from the console, you can press Ctrl+Alt+Delete.

If you are using a terminal emulator like kvt or xterm, you can simply close the window and exit your system as you did before.

If you leave your system logged in (which might be a fine thing to do on your home machine), remember that anyone will be able to see and edit your files. However, never leave a root session open, as this could lead to fatal security problems or even catastrophic user errors.

Typically, Linux systems are left running permanently and only shut down when required by an upgrade or some sort of software malfunction.

## Shutting Down a Linux Box

Shutting down is a bit different from what you might be used to on your PC. Unlike DOS or some other systems, UNIX-like systems need to be shut down gently. Even when no one is logged in, there are a number of processes running. These processes need to be stopped properly, or bad things will happen. Shutting down is accomplished through the shutdown command.

Before you can use the shutdown command, you need to have root privileges. This means that you need to log in as root prior to using the command.

The shutdown command takes a number of arguments. These options specify how the system is going to be shut down and when. The required one in this case are -h, which stands for “halt,” and the keyword now, which specifies that the system should begin shutdown immediately.

To shut down your system gracefully, on a root console, type the following:

```
[root@digital root]# shutdown -h now
```

## Rebooting a Linux Box

Rebooting is just a fancy name for restarting the computer. The shutdown command shown earlier can be used to reboot if you specify the -r option instead of the -h option. The -r option stands for reboot:

```
[root@digital root]# shutdown -r now
```

The easiest way to reboot the system is to simultaneously press the Ctrl+Alt+Del keys, taking the system through the reboot sequence. You can perform this action without being logged in the console.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

## Chapter 12
Working with Files on the Shell

## In This Chapter

- How to Manage and Organize Your Files Using a Shell
- How to Read Files

## Working with Files and Folders

In Chapter 11, “Shells and Consoles,” you learned how to log in and out and how to navigate the file system using a shell. In this chapter you’ll continue your exploration of the UNIX shell and learn how to manipulate files and directories using one.

## Creating a New Empty File: touch

Most of the time you’ll create files as the result of working with some application or shell program. For didactic purposes, I am going to introduce a command that allows you to create empty files here. This ability to generate files as if by magic will make your exploration a little more interesting.

If you need to create an empty file, you can easily do so with the touch command. The purpose of touch is to modify the access and creation times of files, but as a side effect it creates files if they don’t already exist.

To create a file, enter the command touch followed by a filename:

```
[alberto@digital alberto]$ touch afile
```

To verify that the file was created, you might want to use the ls command as explained in Chapter 11.

You can provide more than one filename to the command. Filenames can be specified using relative or absolute paths, or a mix thereof. When the command executes, it creates the specified files.

## Removing Files: rm

To delete a file, you use the rm command. This command is very dangerous for one reason: Files removed under Linux (or UNIX in general) cannot be recovered unless you have a backup on tape, floppy, or some other medium.

To remove a file, type the following:

```
[alberto@digital alberto]$ rm afile
```

The rm command, because of its inherent danger, provides an option that questions any file that you try to remove. If you supply the -i option, it will question your intentions first:

```
[alberto@digital alberto]$ rm -i afile
rm: remove `afile'? y
```

Command aliases are described in Chapter 11 in the section “Making Shell Options the Default.” To see a list of command aliases already active, type alias at the command prompt. A list of all active aliases will be printed for you to inspect.

> Check This Out:
> Oops! I deleted file x rm on tape or another disk, can I get it back?
> Is there a backup on tape or another disk?
> • Yes: yes, you can.
> • No: nope, the file is gone.

## Creating a Directory: mkdir

To create a directory, use the command mkdir and specify the name of the directory (as usual, the name can be a “relative” filename or an absolute path):

```
[alberto@digital alberto]$ mkdir adir
```

If you need to create a entire tree of directories, specify the option -p and the path you need:

```
[alberto@digital alberto]$ mkdir -p
adir/anotherdir/yetanother
```
