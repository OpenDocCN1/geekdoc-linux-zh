# 68 Chapter 14 The TC Shell

The shell you specify is in effect for your next login and subsequent logins until you specify a different login shell. The name of the login shell is stored in the /etc/passwd file.

You can leave tsh in several ways. The way you choose depends on two factors: the shell variable ignoreof is set and whether you are using the shell that you logged in (your login shell) or another shell that you created after you logged in. If you are not sure how to exit from tsh, press CONTROL-D on a line by itself, with no SPACES, just as you would to terminate standard input to another program. You will either exit or receive instructions on how to exit. If you have not set ignoreof (page 712) and it has not been set in one of your startup files (see the next section), you can exit from any shell using CONTROL-D (the same procedure you use to exit the Bourne and Z Shells).

When ignoreof is set, CONTROL-D does not work. The ignoreof variable causes the shell to display a message telling you how to exit. You can always exit from tsh by giving an exit command. A logout command allows you to exit only from your shell.

# Startup Files

When you log in on the TC Shell, it automatically executes various startup files. They are normally executed in the order shown, but you can compile tsh to use a different order.

+   - /etc/csh.login
- /etc/csh.crc

These files contain systemwide configuration information, such as the default path, check for mail, and so on.

+   - ~/.tshrc (or if it does not exist, ~/.tshrc)

This file runs each time a tsh process starts up (the ~ indicates that the file is located in your home directory). You can use the .tshrc file to establish variables and parameters that are local to a shell: Each time you create a new shell, tsh initializes these variables for the new shell. In the following sample .tshrc, the tilde (~) represents the pathname of your home directory (refer to “~ Tilde Expansion” on page 609):

```
tsh $ cat ~/.tshrc
set noclobber
set ignoreof
set history=256
set path = (~/bin $path /usr/games)
alias h history
alias ll ls -1
```

This .tshrc file sets several shell variables, establishes two aliases (page 689), and adds two new directories to path: one at the start of the list and one at the end.