items. The menu is formatted with numbers before each item. For example, a select structure that begins with

```
select fruit in apple banana blueberry kiwi orange watermelon STOP
```

displays the following menu:

```
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon
```

The select structure uses the values of the LINES and COLUMNS variables to determine the size of the display. (LINES has a default value of 24; COLUMNS has a default value of 80.) With COLUMNS set to 20, the menu looks like this:

```
1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP
```

**PS3** After displaying the menu, select displays the value of **PS3**, the special select prompt. The default value of **PS3** is **#** but you typically set **PS3** to a more meaningful value. When you enter a valid number (one in the menu range) in response to the **PS3** prompt, select sets *varname* to the argument corresponding to the number you entered. If you make an invalid entry, *varname* is set to null. Either way select stores your response in the keyword variable **REPLY** and then executes the *commands* between **do** and **done**. If you press **RETURN** without entering a choice, the shell redisplay the menu and the **PS3** prompt.

The select structure continues to issue the **PS3** prompt and execute the *commands* until something causes it to exit—typically a **break** or **exit** statement. A **break** statement exits from the loop and an **exit** statement exits from the script.

The following script illustrates the use of *select*:

```
$ cat fruit2
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry kiwi orange watermelon STOP
do
if [ "$FRUIT" == "" ]; then
echo -e "Invalid entry.\n"
continue
elif [ "$FRUIT" = STOP ]; then
echo "Thanks for playing!"
break
fi
echo "You choose $FRUIT as your favorite."
echo -e "That is choice number $REPLY.\n"
done
```