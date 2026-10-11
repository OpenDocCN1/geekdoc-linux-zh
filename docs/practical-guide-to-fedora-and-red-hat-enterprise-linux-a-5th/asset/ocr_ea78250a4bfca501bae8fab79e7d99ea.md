```
$ cat bbl
set "$*"
echo $# parameters with '$*'
echo 1: $1
echo 2: $2
echo 3: $3

$ bbl a b c
1 parameters with "$*"
1: a b c
2:
3:
```

The bbl2 script shows that set "$@" assigns each argument to a different command-line parameter:

```
$ cat bb2
set "$@"
echo $# parameters with '$@'
echo 1: $1
echo 2: $2
echo 3: $3

$ bb2 a b c
3 parameters with "$@"
1: a
2: b
3: c
```

# shift: PROMOTES COMMAND-LINE ARGUMENTS

The shift builtin promotes each command-line argument. The first argument (which was $1) is discarded. The second argument (which was $2) becomes the first argument (now $1), the third becomes the second, and so on. Because no “unshift” command exists, you cannot bring back arguments that have been discarded. An optional argument to shift specifies the number of positions to shift (and the number of arguments to discard); the default is 1.

The following demo_shift script is called with three arguments. Double quotation marks around the arguments to echo preserve the spacing of the output. The program displays the arguments and shifts them repeatedly until there are no more arguments left to shift:

```
$ cat demo_shift
echo "arg1= $1    arg2= $2    arg3= $3"
shift
echo "arg1= $1    arg2= $2    arg3= $3"
shift
echo "arg1= $1    arg2= $2    arg3= $3"
shift
echo "arg1= $1    arg2= $2    arg3= $3"
shift
```