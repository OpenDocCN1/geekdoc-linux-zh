```
home/me/.bashrc --- [] i(l) i+ 0 1/106 *(/ 338jb) 0635 0x23
# ~/.bashrc executed by bash(l) for non-login shells.
# /usr/share/doc/bash/examples/startup_files (in the package bash-doc)
# for examples
# If not running Interactively, don't do anything
# -z $PS1 && return
# don't duplicate lines or lines with space in the history.
# see bash(1) for more options
HISTCONTROL=ignoredu
# append to the history file, don't overwrite it
shopt -s histappend
# for setting history size use HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000
# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s winsize
#1Help 2Save 3Bark 4Replay 5Copy 6Move 7Search 8Delete 9Wild 10Quit
```

medit

# # Tagging Files

We have already seen how to select a file in the current directory panel by simply moving the highlight, but operating on a single file is not of much use. After all, we can perform those kinds of operations more easily by entering commands directly to the command line. However, we often want to operate on multiple files through tagging. When a file is tagged, it is marked for some later operation such as copying. This is why we choose to use a file manager like Midnight Commander. When one or more files are tagged, file operations (such as copying) are performed on the tagged files and selection has no effect.

# # Tagging Individual Files

To tag an individual file or directory, select it and press the `Insert` key. To untag it, press the `Insert` key again.

# # Tagging Groups of Files

To tag a group of files or directories according to a selection criteria, such as a wildcard pattern, press the + key. This will display a dialog where the pattern may be specified.

Midnight Commander 9