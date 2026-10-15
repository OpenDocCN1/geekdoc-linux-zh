**Table 14.5** File-Testing Operators (continued)

| Test Operator | Tests True If |
|---|---|
| `-u filename` | Set-user-ID bit is set |
| `-w filename` | File is writable |
| `-x filename` | File is executable |

# EXAMPLE 14-26

```
 (The Script)
#!/bin/bash
# Using the old-style test command [ ] single brackets
# filename: perm_check
file=./testing

if [ -d $file ]
then
    echo "$file is a directory"
elif [ -f $file ]
then
    if [ -r $file -a -w $file -a -x $file ]
    then        # nested if command
        echo "You have read,write,and execute permission on $file."
    fi
else
    echo "$file is neither a file nor a directory."
fi

----------------------------------------------------------
#!/bin/bash
# Using the new compound operator for test [[ ]]ᵃ
# filename: perm_check2
file=./testing

if [[ -d $file ]]
then
    echo "$file is a directory"
elif [[ -f $file ]]
then
    if [[ -r $file && -w $file && -x $file ]]
    then        # nested if command
        echo "You have read,write,and execute permission on $file."
    fi
```