# Advanced Bash-Scripting Guide

```
echo

for i    # Omitting the "in list" sets the variable -- i i-
       + to the positional parameters.
do
    echo $i    # Display new positional parameters.
done
IFS=$OLDIFS    # Restore IFS.

# Question Question:
# Is it necessary to set an new IFS, internal field separator,
#+ in order for this script to work properly?
# What happens if you don't? Try it.
# And, why use the new IFS -- a colon -- in line 17,
#+ to append to the loop variable?
# What is the purpose of this?
exit 0

$ ./revposparams.sh
### k0 = a
### k = b

### k0 = a b
### k = c b

### k0 = c a b
### k = d e c b
```

Invoking set without any options or arguments simply lists all the environmental and other variablesnthat have been initialized.

```
bash$ set
AUTHORCOPY=/home/bozo/posts
BASH=/bin/bash
BASH_VERSION='$2.05.8 (1)-release'
...
XAUTHORITY=/home/bozo/.Xauthority
-./etc/bashrc
variable22=abc
variable23=xzy
```

Using set with the -- option explicitly sets the contents of a variable to the positional parameters. If no variable follows the -- it unsets the positional parameters.

# Example 15-18. Reassigning the positional parameters

```
#!/bin/bash
```

Chapter 15. Internal Commands and Builtins 200