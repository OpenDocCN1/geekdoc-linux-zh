files, and those files are read anytime the shell initializes. In multiuser environments, a system will store specific startup files for each username that logs in to the system. Solaris shells use a template system for creating startup resource files. There is usually a systemwide shell resource file for each of the shells that are copied into the home directory. An administrator can modify the template resource file as well as any user's resource file. A user can modify the resource files in their own home directories by adding shell commands to the files. Thus, a user has control over the nature of their environment. The standard Solaris distribution comes with three shells—Bourne, Korn, and C shells—although you can add other shells to the system if you like. By default, the standard shell is the Bourne shell. The Bourne and Korn shells use the `/etc/profile` file as a startup file, and the C shell uses the `.cshrc` and `.login` files. The first time you log in to the C shell, it reads the `.login` file, and any subsequent times you start up a new C shell, it reads the `.cshrc` file.

> **NOTE** The Bourne shell is described in Chapter 18, the Korn shell in Chapter 19, and the C shell in Chapter 20.

The graphical user interfaces such as the Common Desktop Environment (CDE) and OpenWindows are full-featured window managers that offer desktop features. Those environments run on top of X Window sessions. There are many configuration and startup files that set up your environment for these different systems, and those files are described at the beginning of Chapter 7, "The Solaris Desktop." Typically, you use desktop controls in the form of icons that call configuration programs or utilities to change the resource file settings in a window manager. It is possible to modify X Window resource file settings directly, as is described in "Customizing the Desktop" and the sections on the X Window System toward the end of Chapter 7.

# ## Creating Directories and Files

You can create a directory from the command line using the `mkdir` (make directory) command or in the File Manager by using the New Folder command on the File menu. The command-line option is somewhat more powerful, allowing you to create a directory anywhere in the file system with options that even help create a path or set the access privileges for that directory.

The syntax for the `mkdir` command is as follows:

```
`mkdir options (<pathname>)/<directoryname list>`
```