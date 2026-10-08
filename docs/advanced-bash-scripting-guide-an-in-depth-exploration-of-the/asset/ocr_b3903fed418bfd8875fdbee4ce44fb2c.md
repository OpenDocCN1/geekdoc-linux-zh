# Advanced Bash-Scripting Guide

Example 15-8. Problems reading from a pipe

```
#!/bin/sh
# readpipe.sh
# This example contributed by Bjon Eriksson.

### shopt -s lastpipe

last="(null)"
cat $0 |
while read line
do
    echo "${line}"
    last=$line
done

echo
echo "\nall done, last: $last\
```

```
./readpipe.sh
#!/bin/sh
{last="(null)\}
cat $0 |
while read line
do
    echo "${line}"
    last=$line
done
printf "\nall done, last: %s\n" $last"
```

All done, last: (null)

The variable (last) is set within the loop/subshell
but its value does not persist outside the loop.
The gendiff script, usually found in /usr/bin on many Linux distros, pipes the
output of find to a while read construct.

```
find $1 \ -name "*$2" -o -name ".*$2" -print |
while read f; do
```

> It is possible to paste text into the input field of a read (but not multiple lines!). See Example A-38.

# Filesystem

cd

Chapter 15. Internal Commands and Builtins