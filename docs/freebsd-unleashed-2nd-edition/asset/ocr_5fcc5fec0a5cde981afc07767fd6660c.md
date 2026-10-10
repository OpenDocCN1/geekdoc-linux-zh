# **LISTING 11.2** Continued

```
```
#
# Read system messages
# msgrs -f
# Allow terminal messages
# msg y
```
```

Notice that /etc/profile combines the functionality of both /etc/csh.cshrc and /etc/csh.login. It’s the only bash-related global file in the system; there is no systemwide logout script for bash.

The next file for bash is the user’s .profile file, which primarily sets various environment variables (including PATH) and exports them in the Bourne shell style:

```
```
# remove /usr/games and /usr/X11R6/bin if you want
PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/games:/usr/local/bin:/usr/X11R6/bin:$HOME/bin; export PATH
BLOCKSIZE=K;      export BLOCKSIZE
EDITOR=vi;       export EDITOR
PAGER=more;      export PAGER
# set ENV to a file invoked each time sh is started for interactive use.
ENV=$HOME/.shrc; export ENV
```
```

The last line sets the ENV variable to the .shrc file, also in the user’s home directory. This is then read in sequence with .profile. Its purpose is to define the various aliases that tcsh sets in .cshrc, as well as a few other optional things, such as customizing the prompt, that are commented out by default:

```
```
# some useful aliases
alias h='fc -1'
alias j=jobs
alias m=$PAGER
alias ll='ls -laFo'
alias l='ls -l'
alias g='egrep -i'
# # set prompt: `username@hostnamc$
# PS1="\whoami\`@\`hostname | sed 's/\..*//';"
# case `id -u` in
#       0) PS1="${PS1}# ";;
#       \*) PS1="${PS1} ";;
# esac
```
```