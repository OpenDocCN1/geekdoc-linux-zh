# Advanced Bash–Scripting Guide

```
echo
for file in $FILES
do
if [ ! -e "$file" ]    # Check if file exists.
then
    echo "$file does not exist."; echo
    continue
    # On to next.
fi

ls -l $file | awk '{print $9}'    file size: "$5" # Print 2 files.
whatis basename $file    # File info.
echo
done
```

The [list] in a for loop may contain globbing, that is, using wildcards for filename expansion.

# Example 10–4. Operating on files with a for loop

```
#!bin/bash
# list-glob.sh: Generating [list] in a for-loop using "globbing"
echo
for file *
do
    ls -l "$file" # Lists files in $PWD (current directory).
    # Recall that the wild character "* matches everything
    however, in "globbing", it does not match dot-files.

    # If the pattern matches no file, it is expanded to itself.
    # To prevent this, set thes nullglob option
    # (shopt nullglob)
    # Thanks, S.C.
done
echo
for file in []*
do
    rm -f "$file" # Removes only files beginning with "j" or "x" in $PWD.
    echo "Removed file \$file"
done
echo
```

Omitting the [list] in a for loop causes the loop to operate on @$, the list of arguments given on the command line to the script. A particularly clever illustration of this is Example A–14.

# Example 10–5. Missing in [list] in a for loop

Chapter 10. Loops and Branches 104