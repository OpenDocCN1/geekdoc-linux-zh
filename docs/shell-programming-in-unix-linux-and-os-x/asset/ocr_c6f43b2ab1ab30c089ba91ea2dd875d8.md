# Chapter 12 Loose Ends

```
echo "Usage: rem name"
exit 1
fi
```

name=$1

```
#
# Find number of matching entries
#
```

```
matches=$$(grep "$name" \$PHONEBOOK | wc -1)

#
# If than one match, issue message, else remove it
#
```

```
if [ "$matches" -gt 1 ]
then
  echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]
then
  grep -v "$name" \$PHONEBOOK > /tmp/phonebook
mv /tmp/phonebook \$PHONEBOOK
```

echo "I couldn't find $name in the phonebook

```
fi
THE-END-OF-DATA
$
```

To be complete, this archive would include rolo as well, but we didn't include it here to conserve space in the book.

This shell offers one portable file, rolosubs, that contains the source for all three programs lu, add, and rem, can be sent to someone else using mail:

```
$ mail tony@aisystems.com < rolosubs
$ mail tony@aisystems.com
```

Mail the archive
Mail tony a

Tony,

> I mailed you shell archive containing the programs
lu, add, and rem. rolo itself will be sent along shortly.

Pat

```
Ctrl-d
$
```

When tony receives the file in his mail, she can extract the three programs by saving the message, then running the shell on the file (after first removed any email header lines that might have ended up in the beginning of the file):