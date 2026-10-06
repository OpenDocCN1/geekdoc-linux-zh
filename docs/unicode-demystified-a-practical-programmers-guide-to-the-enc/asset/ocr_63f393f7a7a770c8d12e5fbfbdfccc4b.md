# Chapter 15 The Shell and Advanced Shell Programming

your mother or your father or your mother's mother or your father's
mother or father, and so on.
A number of GNU/Linux system utilities can operate recursively. See the -R option
to use the chmod (page 1103) and chown (page 1108) utilities in Part III for examples.
Solve the following problem by using a recursive shell function:

Write a shell function named makepath, given a pathname, creates all the
components in pathname as directories. For example, the command make-path a/b/c/d should create directories a, a/b, a/b/c, and a/b/c/d. (The mkdir-utility supports a -p option that does exactly this. Solve the problem without using mkdir -p.)

One algorithm for a recursive solution follows.

+   1. Examine this path argument. If it is a null string or if it names an existing
directory, do nothing and return.
2. If it is a simple path component, create it (using mkdir) and return.
3. Otherwise, call makepath, using the path prefix of the original argument.
This eventually creates all the directories up to the last component, which
you then create with mkdir.

In general, a recursive function must invoke itself with a simpler version of the
problem than it was given, until finally it gets with a simple case that does not
need to call itself. Here is one possible solution based on this algorithm:

```
# this is a function
# enter it at the keyboard, do not run it as a shell script
makepath()
{
    if [[ ${#1} -eq 0 || -d "$1" ]]
    then
        return 0      # Do nothing
    fi
    if [[ "${1%/*}" = "$1" ]]
    then
        mkdir $1
        return $?
    fi
    makepath ${1%/*} || return 1
    mkdir $1
    return $?
}
```