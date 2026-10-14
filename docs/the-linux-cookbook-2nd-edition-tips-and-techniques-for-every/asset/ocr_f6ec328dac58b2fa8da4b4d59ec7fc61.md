# 3.5.1 Assigning a Variable

To assign a new variable, type its name followed by an equals sign (=) and the quoted string that should become the variable's value. Be sure not to type any space characters on either side of the equals sign.

⇒ To make a new variable called NAME and give it a value of “Mary Jones,” type:

```
$ NAME="Mary Jones" [RET]
```

Values themselves may contain variables, which are then expanded when the variable is assigned. You can use any quoting method to give the value, and you can specify the output of a command (see Recipe 3.1.11 [Specifying the Output of a Command as an Argument], page 65).

⇒ Here are two ways to use this.

+   - To give a variable called NAME a value of the contents of the FIRSTNAME and LASTNAME variables, with a space between them, type:
+     $ NAME="$FIRSTNAME $LASTNAME" [RET]

+   - To give a variable called NAME a value of the output of the whoami command, type:
+     $ NAME=`whoami` [RET]

To change the contents of an existing variable, just give its name as the variable to use.

⇒ To assign a new value to an existing variable called NAME, type:

```
$ NAME="whoami" [RET]
```

This command assigns the value “whoami” to the variable NAME.

# 3.5.2 Referencing a Variable

Reference a variable in a command by preceding its name with a dollar sign ($). When the command is executed, the shell will first substitute the variable word (and the dollar sign) with the value stored in that variable word. This process is called expansion.

⇒ To execute the value of the NAME variable as a command, type:

```
$ $NAME [RET]
mary
$
```