# Chapter 7: Basic Tests

a) Does this script correctly tell whether a file exists?

Answer:Yes it does. Your interaction should look like the following:

```
[7011]: s721 ~/.khshrc
.khshrc does exist.
[7012]: s721 the name_of_a_file_that_does_not_exist
"the name_of_a_file_that_does_not_exist" does not exist.
[7013]:
```

The (-e ) primitive is called a unary operator because it is followed by one operator, and a name that is checked to see whether it is the name of an existing file.

b) What happens if you give s721 the name of a directory instead of the
name of a file?

Answer: If the directory exists, the script will say so, as the following interaction
shows:

```
[7013]: s721 ~/bin
/home/vickery/bin does exist.
[7014]:
```

So, -e does not distinguish between files and directories—it simply tests
for the existence of either one.

Note that the shell has performed "tilde expansion" by substituting the
actual pathname of my home directory for the ~/ before bin. Naturally,
your home directory is not the same as mine, so the pathname you
will be different.

```
# Test a file or directory
if
    [[ -e "$1" ]]
    then if [[ -f "$1" ]]
            then print -- "$1" is a regular file.
        elif [[ -d "$1" ]]
            then print -- "$1" is a directory.
        fi
else
    print -- "\"$1\" does not exist.
fi
```

c) Explain what happens if you run this version of the script with the name
of a file as the parameter.