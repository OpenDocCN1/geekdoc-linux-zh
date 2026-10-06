```
read answer < /dev/tty

if [ "$answer" = y ]; then
    break
fi
done < /tmp/matches$

rm /tmp/matches$

if [ "$answer" != y ]; then
    exit
fi
```

#
# Start editor on the confirmed entry
#

```
echo "$linec" | tr '^' '012' > /tmp/ed$

echo "Enter changes with $[$EDITOR:=/bin/vi]"
trap "* 2 # don't abort DELETE while editing
$EDITOR /tmp/ed$
```

#
# Remove old entry now and insert new one
#

```
grep -v "$line" $PHONEBOOK > /tmp/phonebook$
[ tr '012' < /tmp/ed$$; echo ] >> /tmp/phonebook$
# last echo was to put trailing newline by tr
```

```
sort /tmp/ed$$ -o $PHONEBOOK
rm /tmp/ed$$ /tmp/phonebook$
```

The change program allows the user to edit an entry in the phonebook. The first portion of the code ends up virtually it finds the matching entries and prompts the user to select which one to change.

The selected entry is entered into the temporary file /tmp/ed$, with the ^ characters translated to newlines. This "unfolds" the entry into separate lines to be consistent with how rolo displays the entry for easier editing. The program displays the message
echo "Enter changes with $[$EDITOR:=/bin/vi]",

This serves a dual purpose: it tells the user what editor will be used to make the change and sets the variable EDITOR to /bin/ed vi it is not already set. This technique allows the user to use their preferred editor by assigning its name to the variable EDITOR before executing rolo:

```
$ EDITOR=emacs rolo
```