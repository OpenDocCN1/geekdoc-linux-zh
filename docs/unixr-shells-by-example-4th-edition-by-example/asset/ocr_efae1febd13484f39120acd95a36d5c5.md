# 14.6.2 The $* and $@ Variables in Wordlists

When expanded, the $* and $@ are the same unless enclosed in double quotes. $* evaluates to one string, whereas $@ evaluates to a list of separate words.

# EXAMPLE 14.33

```
(The Script)
#!/bin/bash
# Scriptname: greet
1 for name in $*    # same as for name in $@
2 do
    echo Hi $name
3 done
```

```
(The Command Line)
$ greet Dee Bert Lizzy Tommy
Hi Dee
Hi Bert
Hi Lizzy
Hi Tommy
```

# EXPLANATION

+   1. $* and $@ expand to a list of all the positional parameters, in this case, the arguments passed in from the command line: Dee, Bert, Lizzy, and Tommy. Each name in the list will be assigned, in turn, to the variable name in the for loop.
+   2. The commands in the body of the loop are executed until the list is empty.
+   3. The done keyword marks the end of the loop body.

# EXAMPLE 14.36

```
(The Script)
#!/bin/bash
# Scriptname: permx
1 for file    # Empty wordlist
do
2 if [[ -f $file && ! -x $file ]]
3 then
    chmod +x $file
    echo $file now has execute permission
fi
done
```