+   - Creating personal backup sets in a nightly cron job.
+   - Using sudo to limit user root access.

Let's take a look at how applying these simple prevention measures can help users to recover easily or avoid mistakes like those just discussed.

# Using Aliases to Prevent Data Loss

One of the simplest techniques you can employ is to create aliases for some of the commands that cause users to lose data. Here is an example that is employed by default for the root user on Red Hat systems:

```
# .bashrc

# User specific aliases and functions

alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi
```

Note the three aliases in the .bashrc file for rm, cp, and mv. The -i option to each of these commands requires confirmation by the user before performing a destructive action. In this case, a destructive action would be removing a file with rm or overwriting it with mv or cp. Listing 13.3 shows how the command-line session in Listing 13.1 would have looked if these aliases had been in effect.

# LISTING 13.3 Sample Output Showing How rm Alias Can Prevent Data Loss

```
[tschenk@marc anthony work]$ ls -l
total 96
-rw-r--r-- 1 tschenk staff 14849 Mar 9 00:37 Makefile
-rw-r--r-- 1 tschenk staff 35522 Mar 9 00:37 README
drwxr-xr-x 2 tschenk staff 4096 Mar 9 00:18 docs
-rw-r--r-- 1 tschenk staff 1176 Mar 9 00:37 foobar
-rw-r--r-- 1 tschenk staff 670 Mar 9 00:37 foobar~
-rw-r--r-- 1 tschenk staff 82 Mar 9 00:37 foobaz
drwxr-xr-x 4 tschenk staff 4096 Mar 9 00:22 lib
-rw-r--r-- 1 tschenk staff 866 Mar 9 00:37 line.c
-rw-r--r-- 1 tschenk staff 5956 Mar 9 00:37 main.c
```