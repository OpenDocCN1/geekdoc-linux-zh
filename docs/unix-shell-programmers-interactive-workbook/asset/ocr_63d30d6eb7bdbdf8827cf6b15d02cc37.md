# Chapter 1: SETTING UP 23

At this point, you don't know about functions, aliases, or the set command, which are the commands you would normally put in an environment file, so to get you started, we'll just show you an example without explaining the contents. As you learn more features of the shell, you can develop your own version of this file. Note that the following file contains sample personal preferences that you should modify to match your way of working.

print This is .ksrhc

```
# Set up to use arrow keys for command line editing
EDITOR=vim # Editor to invoke from inside more
VISUAL=emacs # Command line editing style
emacs_keybind # Make arrow keys work
```

# Set up to use less instead of more

```
PAGER=less
export LS='-Eapn?f&?f .?m(File %i of %m) \
..?lt1lb/b%L:?pt&b\:?bt&B/%B:-..?e(end)?xNext:\n%x..
```

# Redefine the ls and rm commands for interactive use.

```
LSFLAGS=-F # Put slashes after directory names, etc.
RMFLAGS=-i # Always ask before deleting files
```

```
alias ls="command ls $LSFLAGS"
alias rm="command rm $RMFLAGS"
```

# Set some shell options

```
set -nolog # Keep function defs out of history file
set -o noclobber # Don't overwrite existing files
```

# Add some command names -- aliases

```
alias="cd .." # Go up one directory
alias m=$PAGER # more (or less)
alias md=mkdir # Like DOS
alias rd=rmdir # Like DOS
alias q=exit #
```

# Add some new command names -- functions