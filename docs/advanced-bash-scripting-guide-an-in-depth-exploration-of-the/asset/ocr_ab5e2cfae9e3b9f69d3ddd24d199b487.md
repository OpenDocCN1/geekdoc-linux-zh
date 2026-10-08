# Advanced Bash-Scripting Guide

on most Linux versions but will probably not work on other shells without modification.

# Introduction
===========

cdll allows easy moving between directories. When changing to a new directory the current one is automatically put onto a stack. By default 50 entries are kept, but this is configurable. Special directories can be kept for easy access - by default up to 10, but this is configurable. The most recent stack entries and the special entries can be easily viewed.

The directory stack and special entries can be saved to, and loaded from, a file. This allows them to be set up on login, saved before logging out or changed when moving to project.

In addition, cdll provides a flexible command prompt facility that allows, for example, a directory name in colour that is truncated from the left if it gets too long.

# Setting up cdll
==========

Copy cdll to either your local home directory or a central directory such as /usr/bin (this will require root access).

Copy the file datafile to your home directory. It will require and write access. This default file contains a directory stack and special entries.

To replace the cd command you must add commands to your login script. The login script is one or of:

```
/etc/profile
~/bash_profile
~/bash_login
~/profile
~/bashrc
/etc/bash.bashrc.local
```

To set up login, ~/.bashrc is recommended, for global (and root) setup add the commands to /etc/bash.bashrc.local

+   Set up on login, add the command:
- <dir>/cdll
- For example if cdll is in your local directory:
- ~/cdll
- If in /usr/bin then:
- /usr/bin/cdll

If you want to use this of the builtin cd command then add:
alias cd='cd_new'
We would also recommend the following commands:

+   - cd -U
- cd -D

If you want to use cdll's prompt facil then add the following:
CDL_PROMPTLEN=nn
Where nn is a number described below. Initially 99 would be suitable number.

# Appendix A. Contributed Scripts