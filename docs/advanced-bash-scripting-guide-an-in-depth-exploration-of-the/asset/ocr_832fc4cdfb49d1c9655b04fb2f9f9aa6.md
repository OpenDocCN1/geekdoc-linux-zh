# Chapter 32. Debugging

Debugging is twice as hard as writing the code in the first place. Therefore, if you write the code as cleverly as possible, you are, by definition, not smart enough to debug it.

> --Brian Kernigh

The Bash shell contains no built-in debugger, and only bare-bones debugging-specific commands and constructs. Syntax errors or ought typos in the script generate cryptic error messages that are often of no help in debugging a non-functional script.

# Example 32-1. A buggy script

```
#!/bin/bash
# ex7.sh

# This is a buggy script.
# Where, oh where is the error?
a=37

if [$a -gt 2 ];
then
echo $a
fi

exit $? # 0! Why?
```

Output from script:
./ex7.sh: [37]: command not found
What's wrong with the above script? Hint: after the if.

# Example 32-2. Missing keyword

```
#!/bin/bash
# missing-keyword.sh
# What error message will this script generate? And why?
for a in 1 2 3
do
echo "$a"
# Required keyword 'done' commented out in line 8.
done

exit 0
# # Will not exit here!
# -----
# From command line, after script terminates.
echo $? # 2
```

Output from script:
missing-keyword.sh: line 10: syntax error: unexpected end of file

Chapter 32. Debugging 476