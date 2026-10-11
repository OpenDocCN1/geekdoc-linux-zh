# Using Positional Parameters

We cover the use of variables later in this chapter, but a special set of vari-
ables exists for every program or script that is run. These are called *position-
al parameters*. A positional parameter is a variable named with a single
numeral, such as $1, $2, and $3. The $ symbol is how you access and expand
the variable on the command line.

Positional parameters are typically numbered from 1 to 9 (any of these num-
bers can be used) and begin after any options for the program. For example,
to specify three color options for a program, you would use the positional
parameters:

```
command blue red green
```

In this command, the *command* stands alone, while *blue* becomes $1, *red*
becomes $2, and *green* becomes $3.

These parameters are useful when you want to have an overall script that can
be customized by what you specify as an input variable, such as

```
#!/bin/bash
# filename: au
# Create a user, username read from $1, shell from $2
useradd -m -s /bin/$2 $1
```

You then run the script with the arguments $1 and $2 being the target user-
name and shell:

```
./au rbrunson sh
```

You can then run it many times with different usernames and shell values.
This is a very simple example; use your imagination to make this much more
useful.

The positional parameter $7 shows the most recently executed program’s sta-
tus. It shows a value of 0 if it succeeded without errors and a non-zero value
if it had errors or failed to execute.

The final positional parameter to discuss is $0, which reflects the name of the
script or program that is running. For example, if you ran the script *script1*,
the $0 would echo back *script1*:

```
#!/bin/bash
echo "$0 is the program"
```