# Creating the home directory and installing startup files

```
$ sudo passwd newusername
```

You'll be prompted for the actual password. Some automated systems for adding new users do not require you to provide an initial password. Instead, they force the user to set a password on first login. Although this feature is convenient, it's a giant security hole: anyone who can guess new login names (or look them up in /etc/passwd) can sweep down and hijack the accounts before the intended users have had a chance to log in.

# Creating the home directory and installing startup files

You can create the new user's home directory with a simple mkdir. You'll need to set ownerships and permissions on the new directory as well, but this is best done after you've installed local startup files.

Startup files traditionally begin with a dot and end with the letters rc

We recommend that you provide default startup files for each shell that is popular on your systems so that users continue to have a reasonable default environment if they change shells. 7.3 lists some common startup files.

# Table 7.3 Common startup files and their uses

| Command | Filename | Typical uses |
| --- | --- | --- |
| sh | .profile | Sets search path, terminal type and environment |
| bashᵃ | .bashrc | Sets the terminal type (if needed)<br>Sets biff and mesg switches<br>Sets up environment variables<br>Sets command aliases<br>Sets the search path<br>Sets the umask value to control permissions<br>Sets CDPATH for filename searches<br>Sets the PS1 (prompt) and HISTCONTROL variables |
| csh/tcsh | .login .cshrc | Similar to .bashrc for csh<br>Similar to .login for csh |
| vi/vim | .exrc/.vimrc | Sets vi/vim editor options |
| emacs | .emacs | Sets emacs editor options and key bindings |
| mail/mailx | .mailrc | Defines personal mail aliases<br>Sets mail reader options (original UNIX mail client) |
| GNOME | .gconf .gconfpath | GNOME environment: user configuration via gconf<br>Path for additional user configuration via gconf |
| KDE | .kde/ | KDE environment: directory of configuration |

ᵃ bash also reads .profile or /etc/passwd in emulation of sh.