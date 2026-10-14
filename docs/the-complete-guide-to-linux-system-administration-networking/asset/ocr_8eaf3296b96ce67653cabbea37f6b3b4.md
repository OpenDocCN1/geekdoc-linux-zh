Don't confuse the forward single quotes used to prevent command-line substitution ( ' ) with the reverse single quotes (back quotes) used to cause command substitution ( ` ). The forward single quote is usually located next to the Enter or Return key on the keyboard; the location of the reverse single quote varies, but may be located in the upper left, next to the number 1, or near either end of the spacebar.

A third form of protection against unwanted command-line substitution is the use of double quotes—standard quotation marks. Using these has nearly the same effect as single quotes, but some special characters are still interpreted by the shell rather than being used literally. When you use single quotes, everything between them is interpreted literally; when you use double-quotes, everything between them is interpreted literally except the following:

+   - $ Used to signal the start of a variable
+   - ` Used to signal the start of a command substitution
+   - \$ Used to output a $ character
+   - \` Used to output a ` character
+   - \" Used to output a " character
+   - \\ Used to output a \ character

So, for example, some parts of the following command are interpreted as special characters, and some parts are interpreted literally, as shown by the output:

```
$ echo "$USER has entered a \"value\" over \$500;
this is not a valid entry."
```

James has entered a "value" over $500; this is not a valid entry.

Compare the above example to the output if single quotes were used instead of double quotes:

```
$ echo '$USER has entered a \"value\" over \$500;'
this is not a valid entry.'
```

$USER has entered a \"value\" over \$500;
this is not a valid entry.

Figuring out exactly how the shell substitutes various characters in a complex command-line statement can be challenging, even for experienced system administrators. By experimenting with different combinations, you can learn how to get the results you are expecting. Although it doesn't have a lot of examples to guide you, a valuable reference is the man page for the bash shell. You can view this by entering the command man bash.