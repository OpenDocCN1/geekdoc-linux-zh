# Control Structures 659

```
$ cat fruit
!/bin/bash
PS3=Choose your favorite fruit from these possibilities: ""
select FRUIT in apple banana blueberry orange watermelon STOP
do
if [$FRUIT = STOP]; then

echo "Thanks for playing!"
break
fi
echo echoYou chose number $FRUIT as your favorite."
echo
done
```

+   $ fruit
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

Choose your favorite fruit from these possibilities:
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities:
An invalid menu choice causes zsh to assign a null string to varname and execute the commands between do and done. If the user presses RETURN without entering a choice, the Z Shell replays the menu and the PS3 prompt. The Z Shell stores the user's response in the keyword variable REPLY.
as the syntax indicates, you can omit the keyword in the list of arguments. If you do, select uses the current values of the positional parameters $@.

# Here Document

A here document allows you to redirect input to a shell script from within the shell script itself. A here document is so called it here, immediately accessible in the shell script, instead of there, perhaps in another file.
The following script, birthday, contains a Here document. The two less (<<) symbols in the first line indicate to the shell that a Here document follows. One or more characters that delimit the Here document follow the less signs—this example uses plus signs. Whereas the opening delimiter can occur adjacent to the less signs, the closing delimiter must occur on a line by itself. The shell sends everything between the two delimiters to the process as standard input. In the following example it is as as though you had redirected standard input to grep from a file, except that the file is embedded in the shell script:

The term Here document is not used in the zan man pages; you must search for << instead.

![](bbox=[0.355, 0.603, 0.395, 0.633])