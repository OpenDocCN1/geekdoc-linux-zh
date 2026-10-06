# Startup Files (Continued)

| /etc/zshrc | This file is created by Superuser to establish systemwide default characteristics for zsh interactive shells (where standard input and standard output are both connected to a terminal). This file is not read when zsh is called with the -f option |
| ~/.zshrc | You create this file in your home directory. This file is read only by interactive shells (where standard input and standard output are both connected to a terminal) and is not read when zsh is called with the -f option |
| /etc/zlogin | This file is created by Superuser to establish systemwide default characteristics for zsh login shells. This file is read when a login starts up (or when zsh is called with the -l option) but not when the -f option is used. It is the preferred file for systemwide characteristics for users desiring a C- or TC-like shell |
| ~/.zlogin | You create this file in your home directory. This file is the preferred location to set variables that override those set in /etc/zlogin and when a login shell starts up (or when zsh is called with the -l option) but not when the -f option is used. It is the preferred file for setting characteristics for users desiring a C- or TC-like shell.

Because .zhenv is the only file used for zsh initialization except when you use -f), you can place all your variable initializations and option setups in this file. How you use the other startup files depends on how you use zsh: Is the invocation of zsh login shell and/or an interactive shell? Sample .zhenv, .profile, and .zrc files follow. Some of the commands used in these files are not covered later in this chapter. In any of the startup files, functions that you want to be able to process:

```
% cat .zhenv
MAIL=/usr/spool/mail/${LOGIN}?
MANPATH=/usr/man:/usr/X11R6:/usr/local/man
PATH=$HOME/bin:/usr/local/bin:/usr/bin/X11:/usr/bin:/bin:
export MAIL MANPATH PATH
umask 002
% cat .profile
FCEDIT=/usr/bin/vim
PS1='$ '
PS2='>
HISTSIZE=256
stty kill '^u' erase '^h' intr '^Ac' quit '^\'
export FCEDIT PS1 PS2 HISTSIZE
```