# Chapter 9 Reading and Printing Data

Please select one of the above (1-3): 4

Bad choice
$

When an invalid choice is entered, the program displays Bad choice and terminates.
A friendly approach would be to loop around and again prompt the user to a proper choice
is made. This can be done by enclosing the entire program inside a loop that will be
executed until a valid selection is made.

Another change to rolo reflects its most likely usage: Because the most common operation
is looking someone up, there will be a tendency to avoid typing rolo, then making selection
i, then the desired name. Instead, it's a little easier to just type in

lu name
directly, let's give role some command line arguments so it can also be
used efficiently. By default any arguments are specified, rolo will assume a lookup
requested and call lu directly, handling all the arguments along. If the user wants to perform
a quick lookup, they can type rolo followed by the name. If they want to get the full menu
interface, they type rolo offers just that alternative.

The preceding two changes (looping until a valid choice is selected and doing a quick lookup)
are added to version 2 of rolo:

```
$ cat rolo
#
# rolo - rolodex program to look up, add, and
#   remove people from the phone book -- version 2
#

# If arguments are supplied, then do a lookup
#

if [ "$#" -ne 0 ]; then
    lu "$@"
    exit
fi
validchoice="    # set it null
#
# Loop until a valid selection is made
#

until [ -n "$validchoice" ];
do
    #
    # Display menu
    #
```