```
sort -o $PHONEBOOK $PHONEBOOK
$ cat lu
#
# Look up someone in the phone book
#
if [ "$1" -ne 1 ]; then
    echo "Incorrect number of arguments"
    echo "Usage: lu name"
    exit 1
fi

name=$1
grep "$name" $PHONEBOOK

if [ $7 -ne 0 ]; then
    echo "I couldn't find $name in the phone book"
fi
$ cat rem
#
# Remove someone from the phone book
#
if [ "$#" -ne 1 ]; then
    echo "Incorrect number of arguments"
    echo "Usage: rem name"
    exit 1
fi

name=$1
#
# Find number of matching entries
#
matches=$(grep "$name" $PHONEBOOK | wc -1)
#
# If more than one match, issue message, else remove it
#
if [ "$matches" -gt 1 ]; then
    echo "More than one match; please qualify further"
elif [ "$matches" -eq 1 ]; then
    grep -v "$name" $PHONEBOOK > /tmp/phonebook$$
    mv /tmp/phonebook$$ $PHONEBOOK
else
```