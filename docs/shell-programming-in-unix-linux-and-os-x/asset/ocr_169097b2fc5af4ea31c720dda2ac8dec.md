```
#
# See if destination file is a directory
#
if [ -d "$to" ]; then
nto="$to/\$(basename $from)*"
fi

# See if the destination file already exists
#
if [ -e "$to" ]; then
  echo "$to already exists; overwrite (yes/no)? \c"
  read answer

  if [ "$answer" = yes ]; then
    echo "Copy not performed"
    exit 0
  fi
fi

# Either destination doesn't exist or "yes" was typed
#
cp $from $to # proceed with the copy
```

If the destination file is a directory, the program changes the variable `to` to more precisely identify the destination filename by including the directory name: `to/$(basename $from)`. This ensures that the subsequent test for the existence of the ordinary file `$to` will be done on the file in the directory, not on the directory itself.

The basename command gets the base filename of its argument with all directory components stripped away (for example, basename /usr/bin/troff produces troff; basename been produces troph). This extra step ensures that the copy is made from and to the correct place. (As example, if mycp `/tmp/data bin` is typed, where bin is a directory, you want to copy `/tmp/data` into `bin/data` and not into `bin/tmp/data.)

Here's some sample output. Note the effect of the \c escape characters.

```
$1
Check out current directory
bin
progl
$1 bin
Look inside bin
lu
nu
progl
```