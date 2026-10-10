# Part IV: Working with Alternative Shells

> **Note**
> Some Linux distributions (such as Debian) create a zsh directory under the /etc directory to contain all of the zsh shell startup files, instead of placing them directly in the /etc folder.

# The shell login files

If you use the zsh shell as a login shell, it first looks for and executes two files:

+   - /etc/zlogin
+   - /etc/zprofile

These files are executed for all users who use the zsh shell as their login shell. The files should contain system-wide environment variables that should be set for all users and executable programs that all users should use (such as the *umask* command to set default file and directory permissions). Most likely if you’re using a Linux distribution that supports the zsh shell, these files already exist for setting system environment variables at login.

After executing this file, the zsh shell looks for two files in each user’s *$HOME* directory:

+   - *$HOME*/.zlogin
+   - *$HOME*/.zprofile

These files can contain user-specific environment variable settings and executable commands that an individual user wants to run when logging in to the system, before the command line interface prompt appears.

Any environment variable settings you make in the *$HOME* /.zprofile shell will override any system-wide settings made in the */etc/zprofile* file, and similarly for the *.zlogin* files. You can test the order in which the zsh shell executes these files by adding a simple *echo* statement to each one and then logging in:

```
```
$ zsh -l
This is the /etc/zshenv file.
This is the .zshenv file in HOME.
This is the /etc/zprofile file.
This is the .zprofile file in HOME.
This is the /etc/zlogin file.
This is the .zlogin file in HOME.
$ 
```
```

As you can see from the example, the zsh shell executes the *zshenv* files first, then the *zprofile* files, and finally the *zlogin* files.

# The interactive shell files

If you start an interactive zsh shell session, there’s another set of files that can hold startup variables and commands:

+   - /etc/zshrc
+   - *$HOME*/.zshrc