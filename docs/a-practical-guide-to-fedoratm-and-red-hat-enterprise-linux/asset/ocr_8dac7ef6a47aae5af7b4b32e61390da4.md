```
```sh
$ date
Wed Aug 15 17:35:29 PDT 2012
$ cat dataset
set $(date)
echo $
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 6: $6"
echo
     echo "$2 $3, $6"

$ ./dataset
Wed Aug 15 17:35:34 PDT 2012

Argument 1: Wed
Argument 2: Aug
Argument 3: 15
Argument 6: 2012

Aug 15, 2012
```
```

You can also use the +format argument to date to specify the content and format of its output.

When called without arguments, set displays a list of the shell variables that are set, including user-created variables and keyword variables. Under bash, this list is the same as that displayed by declare (page 357) when it is called without any arguments.

```
```bash
$ set
BASH_VERSION='4.2.24(1)-release'
COLORS=/etc/DIR_COLORS
COLUMNS=89
LESSOPEN=" | /usr/bin/lesspipe.sh %s"
LINES=53
LOGNAME=sam
MAIL=/var/spool/mail/sam
MAILCHECK=60
...
```
```

The set builtin can also perform other tasks. For more information refer to “set: Works with Shell Features, Positional Parameters, and Variables” on page 1036.

# ### shift: PROMOTES POSITIONAL PARAMETERS

The shift builtin promotes each positional parameter. The first argument (which was represented by $1) is discarded. The second argument (which was represented by $2) becomes the first argument (now $1), the third argument becomes the second, and so on. Because no “unshift” command exists, you cannot bring back arguments that have been discarded. An optional argument to shift specifies the number of positions to shift (and the number of arguments to discard); the default is 1.