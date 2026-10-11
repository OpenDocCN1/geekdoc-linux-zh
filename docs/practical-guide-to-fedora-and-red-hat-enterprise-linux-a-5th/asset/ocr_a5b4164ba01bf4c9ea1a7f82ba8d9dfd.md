```
$ cat case2
echo -n "Enter A, B, or C: "
read letter
case "$letter" in
a|A)
echo "You entered A"
;;
b|B)
echo "You entered B"
;;
c|C)
echo "You entered C"
;;
*)
echo "You did not enter A, B, or C"
;;
esac

$ case2
Enter A, B, or C: b
You entered B
```

Table 27-2   Patterns

| Pattern | Function |
| :--- | :--- |
| \* | Matches any string of characters. Use for the default case. |
| ? | Matches any single character. |
| [...] | Defines a character class. Any characters enclosed within brackets are tried, one at a time, in an attempt to match a single character. A hyphen between two characters specifies a range of characters. |
| | | Separates alternative choices that satisfy a particular branch of the case structure. |

**optional**   The following example shows how you can use the **case** structure to create a simple menu. The **command\_menu** script uses **echo** to present menu items and prompt the user for a selection. (The **select** control structure [page 917] makes it much easier to code a menu.) The **case** structure then executes the appropriate utility depending on the user’s selection.

```
$ cat command_menu
#!/bin/bash
# menu interface to simple commands

echo -e "\n\t\tCOMMAND MENU\n"
echo "	a. Current date and time"
echo "	b. Users currently logged in"
echo "	c. Name of the working directory"
echo -e "	d. Contents of the working directory\n"
echo -n "Enter a, b, c, or d: "
read answer
echo
```