```
$ myname=ralph
$ echo "My name is $myname"
My name is ralph
```

There may be times when the shell can become confused if the variable name is not easily identified in the command line:

```
$ string=dobeedobee
$ echo "$stringdoo"
```

We wanted to display "dobeedobee," but the shell thought the variable name was stringdoo, which had no value. To accomplish this we can use curly braces around the variable name to separate it from surrounding characters:

```
$ echo "${string}doo"
dobeedobeedoo
```

You can set variables in shell programs in the same way, but you would also like to do things such as save the output of a command in a variable so that we can use it later. You may want to ask users a question and read their response into a variable so that you can examine it.

# Command Substitution

Command substitution allows us to save the output from a command (**stdout**) into a shell variable. To demonstrate this, let’s take another look at how our “today” example can be done using command substitution.

```
#!/bin/ksh
d=`date +%x`
echo "Today's date is $d"
```