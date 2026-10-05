# 984 CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

items. The menu is formatted with numbers before each item. For example, a select structure that begins with

select fruit in apple banana kiwi orange watermelon STOP
displays the following:

+   1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

The select structure uses the values of the LINES and COLUMNS variables to specify the size of the display. (LINES has a default value of 24; COLUMNS has a default value of 80.) With COLUMNS set to 20, the menu looks looks like this:

+   1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

PS3 After displaying the menu, select displays value of PS3, the select prompt. The default value of PS3 is #?, but it is typically to a more meaningful value. When you enter a value (one in the range) and response to the PS3 prompt, select varname to the argument corresponding to the number you entered. An invalid entry causes the shell to set varname to null. Either way stores your response in the keyword variable REPLY and then executes the commands between do and done. If you press RETURN without entering a choice, the shell redisplays the menu and the PS3 prompt.

The select structure continues to issue the PS3 prompt and execute the commands until it causes it to exit—typically a break or exit statement. A break statement exits from the loop and an exit statement from the script.

The following script illustrates the use of select:

```
$ fruit2
#/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry kiwi orange watermelon
done
if [ "$FRUIT" = "" ]; then
    echo -e "Invalid entry.\n"
    continue
elif [ $FRUIT = STOP ]; then
    echo "Thanks for playing!"
    break
fi
echo "You chose $FRUIT as your favorite"
echo -e "That is choice number $REPLY.\n"
done
```