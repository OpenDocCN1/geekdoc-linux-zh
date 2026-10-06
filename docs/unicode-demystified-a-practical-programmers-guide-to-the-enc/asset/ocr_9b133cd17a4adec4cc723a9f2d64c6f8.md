```
if [ -r "$1" -w "$1" ]
then
    echo "$script: check permissions on $1" >&2
    exit 1
else
    editfile=$1
fi
if [ ! -w "." ]
then
    echo "$script: backup cannot be " \
        "created in the working directory" >&2
    exit 1
fi
*)
    ;
    echo "Usage: $script [file-to-edit]" >&2
    exit 1
    fi
esac
tempfile=/tmp/$.script
cp $editfile $tempfile
if vi $editfile
then
    mv $tempfile bak.$(basename $editfile)
    echo "$script: backup file created"
else
    mv $tempfile editerr
    echo "$script: edit error--copy-of " \
        "original file is in editerr" >&2
fi
```

If you call safedit without any arguments, the *case* structure executes its first branch and calls vi without a filename. Because an existing file is not being edited, *safedit* does not create a backup file. (See the :w command on page 426 for an explanation of how to exit from vi when you have called it without a filename.) If the user calls *safedit* with one argument, the script runs in the second branch of the case structure and verifies that the file specified by $1 does not exist or is the name of a file for which the user has read and write permission. The safedit script also verifies that the user has write permission for the working directory. If the user calls *safedit* with more than one argument, the third branch of the *case* structure presents a usage message and exits with a status of 1.

In addition to the use of a *case* structure for branching based on the number of command line arguments, the *safedit* script introduces several other features. At the beginning of the script, the PATH variable is set to search /bin and /usr/bin. This ensures that the commands executed by the script are standard utilities, which are kept in those directories. By setting PATH inside a script, you can avoid the problems that might occur if users have set up PATH to search their own directories first and have scripts or programs with the same names as utilities the script uses.

Second, the following line creates a variable named *script* and assigns the simple filename of the script to it: