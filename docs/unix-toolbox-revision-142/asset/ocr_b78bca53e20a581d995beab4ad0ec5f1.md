# FreeBSD

```
Quotas for user colin:
/home: kbytes in use: 504184, limits (soft = 700000, hard = 800000)
    inodes in use: 1792, limits (soft = 0, hard = 0)
```

# For many users

The command edquota -p is used to duplicate a quota to other users. For example to duplicate a reference quota to all users:

```
# edquota -p refuser `awk -F: '$3 > 499 {print $1}' /etc/passwd`
# edquota -p refuser user1 user2   # Duplicate to 2 users
```

# Checks

Users can check their quota by simply typing quota (the file quota.user must be readable). Root can check all quotas.

```
# quota -u colin                # Check quota for a user
# repquota /home                # Full report for the partition for all users
```

# 20 SHELLS

Most Linux distributions use the bash shell while the BSDs use tcsh, the bourne shell is only used for scripts. Filters are very useful and can be piped:

+   grep Pattern matching
+   sed Search and Replace strings or characters
+   cut Print specific columns from a marker
+   sort Sort alphabetically or numerically
+   uniq Remove duplicate lines from a file

For example used all at once:

```
# ifconfig | sed 's/ / /g' | cut -d" " -f1 | uniq | grep -E "[a-z0-9]+" | sort -r
# ifconfig | sed '/inet addr:/!d;s/.*//.*/'|sort -t. -k1,1n -k2,2n -k3,3n -k4,4n
```

The first character in the sed pattern is a tab. To write a tab on the console, use ctrl-v ctrl-tab.

# 20.1 bash

Redirects and pipes for bash and sh:

```
# cmd1 > file                 # Redirect stdout to file.
# cmd2 > file                 # Redirect stderr to file.
# cmd1 >> file                # Redirect and append stdout to file.
# cmd1 <> file                # Redirect both stdout and stderr to file.
# cmd1 >file 2>&1             # Redirects stderr to stdout and then to file.
# cmd1 | cmd2                 # pipe stdout to cmd2
# cmd1 2>&1 | cmd2            # pipe stdout and stderr to cmd2
```

Modify your configuration in ~/.bashrc (it can also be ~/.bash_profile). The following entries are useful, reload with ". ~/.bashrc". With cygwin use ~/.bash_profile; with rxvt past with shift + left-click.

```
# in .bashrc
bind "\e[A":history-search-backward  # Use up and down arrow to search
bind "\e[B":history-search-forward    # the history. Invaluable!
set -o emacs                         # Set emacs mode in bash (see below)
set bell-style visible               # Do not beep, inverse colors
# Set a nice prompt like [user@host]/path/todir>
PS1="\[\033[1;30m\]\[\033[1;34m\]u@\[\033[1;30m\]"
PS1="$PS1\[\033[0;33m\]\w\[\033[1;33m\]1\[\033[0;37m\]"
PS1="$PS1\w\[\033[1;30m\]>\[\033[0m\]"
# To check the currently active aliases, simply type alias
alias ls='ls -af'                    # Append indicator (one of */=>@l)
```