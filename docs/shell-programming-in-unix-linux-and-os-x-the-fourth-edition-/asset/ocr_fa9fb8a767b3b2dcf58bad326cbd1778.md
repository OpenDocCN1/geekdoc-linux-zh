```
if [ "$#" -ne 2 ] ; then
    echo "Usage: mycp from to"
    exit 1
fi

from="$1"
to="$2"

#
# See if the destination file already exists
#

if [ -e "$to" ] ; then
    echo "$to already exists; overwrite (yes/no)?"
    read answer

    if [ "$answer" != yes ] ; then
        echo "Copy not performed"
        exit 0
    fi
fi

#
# Either destination doesn't exist or "yes" was typed
#

cp $from $to      # proceed with the copy
$
```

Now let’s give the program a quick test:

```
$ ls -c                         What files? -C forces multicolumn output too
Addresses       intro       lotsaspaces      mycp
names           nu          numbers          phonebook
stat
$ mycp                          No arguments
Usage: mycp from to
$ mycp names names2              Make a copy of names
$ ls -l names*                   Did it work?
-rw-r--r--  1 steve  steve      43 Jul 20 11:12 names
-rw-r--r--  1 steve  steve      43 Jul 21 14:14 names2
$ mycp names numbers             Try to overwrite an existing file
numbers already exists; overwrite (yes/no)?
no
Copy not performed
$
```