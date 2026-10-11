The `\n` string in the first `echo` statement is interpreted as newline characters. This is one of the formatting characters you have available to you. To make the menu more readable, it helps to include formatting characters. Other characters that may be useful in creating menus are `\b` (backspace), `\c` (suppresses trailing newline), `\f` (formfeed), `\n` (newline), `\r` (return), `\t` (horizontal tab), and `\v` (vertical tab).

The `case control` structure will branch to different actions depending upon the number of arguments on the command line. The following example demonstrates how `case` treats a `vi` editor file while branching several arguments:

```
```
$ cat filedit2
#!/bin/sh
# Patterned after filedit by S. King edited by J. Newbury
# Hobgoblins, VIII:2 p 233, summary

PATH=/bin:/usr/bin
Script="basename $0"

case $# in
0)
    vi
    exit 0
;;
1)
    if [ ! -f '$1' ]
    then
        vi "$1"
    elif [ ! -r '$1' -o ! -w '$1' ]
    then
        echo "$Script: check permissions "\
'on $1' 1>&2
        exit 1
    elif [ ! -w "." ]
    then
        echo "$Script: backup cannot be "\
'created in the working ' \
'directory' 1>&2
        exit 1
    else
        editfile=$1
```
```