```
```text
Please select one of the above (1-3): 4
Bad choice
$
```
```

When an invalid choice is entered, the program displays Bad choice and then terminates. A friendlier approach would be to loop around and again prompt the user until a proper choice is made. This can be done by enclosing the entire program inside an until loop that will be executed until a valid selection is made.

Another change to `rolo` reflects its most likely usage: Because the most common operation will be looking someone up, there will be a tendency to avoid typing `rolo`, then making selection 1, then typing the desired name. Instead, it’s a lot easier to just type in

```
```text
lu name
```
```

directly. Given this, let’s give `rolo` some useful command line arguments so it can also be used as efficiently. By default if any arguments are specified, `rolo` will assume that a lookup is requested and call `lu` directly, handling all the arguments along. If the user wants to perform a quick lookup, they can type `rolo` followed by the name. If they want to get the full menu interface, typing just `rolo` offers just that alternative too.

The preceding two changes (looping until a valid choice is selected and doing a quick lookup) are added to version 2 of rolo:

```
```sh
$ cat rolo
#
# rolo - rolodex program to look up, add, and
#     remove people from the phone book -- version 2

#
# If arguments are supplied, then do a lookup
#

if [ "$#" -ne 0 ]; then
        lu "$@"
        exit
fi

validchoice=""        # set it null

#
# Loop until a valid selection is made
#

until [ -n "$validchoice" ]
do
        #
        # Display menu
        #
```
```