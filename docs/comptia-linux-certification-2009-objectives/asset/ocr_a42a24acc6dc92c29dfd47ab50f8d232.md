![](bbox=[0.053, 0.104, 0.124, 0.148])

Search Paths

# # Search Paths

# ## Definition:

A *search path* is a sequence of various directory paths that is used by the shell to locate files. Paths can be assigned to the *PATH* environment variable. The *PATH* variable comprises a list of directory names separated by colons. You can add a new path to an existing group of path names, modify a path, or delete a path. Usually directories that contain executable files are assigned to the *PATH* variable.

*root@localhost:*

```
```bash
# User specific aliases and functions
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
# Source global definitions
if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi
# User specific environment and startup programs
PS1=" [ Our Global Company \u ] "
PATH=$PATH:/root
HISTSIZE=100
export PS1 PATH HISTSIZE
```"
```

PATH variable

Figure 9-12: A search path defined in the .bashrc file.

# ### Example:

The following is an example of a search path where the path names are separated by colons:

/home/user/bin:/usr/local/bin:/usr/bin:/bin

# ### Non-Example:

The following is not a search path because the path names are not separated by colons:

/usr/bin /usr/local/bin