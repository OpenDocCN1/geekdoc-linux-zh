```
if [ -n "$2" ]
then
echo "Parameter #2 is $2"
fi

if [ -n "$3" ]
then
echo "Parameter #3 is $3"
fi

...
if [ -n "$10" ] # Parameters > $9 must be enclosed in (brackets)
then
echo "Parameter #10 is $10"
fi
```

Some scripts can perform different operations, depending on which name they are invoked. For this work, the script needs to check $0, the name it was invoked. There must also exist symbolic links to all the alternate names of the script.

> If a script expects a command line parameter but is invoked without one, this may cause a null variable assignment, generally an undesirable result. One way to prevent this is to append an extra character to both sides of the assignment statement using the expected positional parameter.

```
variable1=$1_
# Will prevent an error, even if positional parameter is absent.
critical_argument01=$variable1

# The extra character can be stripped off later, if desired, like so.
variable1=${variable1/} # Side effects only if $variable1 begins with "_"
# This uses one of parameter substitution templates discussed in Chapter 9.
# Leaving the replacement pattern results in a deletion.

# A more straightforward way of dealing with this is
# to simply test whether expected positional parameters have been passed.
if [ -z $1 ]
then
  exit POS_PARAMS_MISSING
fi
```

Example 5–6. wh, whois domain name lookup

```
#!/bin/bash
```

# 5.4. Special Variable Types