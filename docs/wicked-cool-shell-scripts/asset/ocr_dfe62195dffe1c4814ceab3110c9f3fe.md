```
exit 1
fi

if [ $# -eq 0 ] ; then
# Display the whole rememberfile when not given any search criteria.
more $rememberfile
else
# Otherwise, search through the file for the given terms, and display
# the results neatly.
grep -i -- "$@" $rememberfile | ${PAGER:-more}
fi

exit 0
```

Listing 3-2: The remindme shell script, a companion to the remember shell script in Listing 3-1

# How It Works

The remember shell script in Listing 3-1 can work as an interactive program, requesting the user to enter the details to remember, or it could actually be scripted since it can also accept anything to store simply as a command line argument. If a user does not pass any arguments to the script, then we do a little tricky coding. After printing a user-friendly message on how to enter an item, we read the data from the user with cat ①:

```
cat - >> $rememberfile
```

In previous chapters, we have used the read command to get input from the user. This line of code reads from stdin (the - in the command is shorthand for stdin or stdout, depending on the context) using cat until the user presses CTRL-D, which tells the cat utility that the file has ended. As cat prints the data it reads from stdin, and appends this data to the rememberfile.

If an argument is specified to the script, however, all arguments are simply appended as is to the rememberfile ②.

The remindme script in Listing 3-2 cannot work if the rememberfile doesn’t exist, so we first check if the rememberfile exists before attempting to do anything. If the rememberfile doesn’t exist, we exit immediately after printing a message to the screen alerting the user why.

If no arguments are passed to the script, we assume the user just wants to see the contents of the rememberfile. Using the more utility to allow paging through the rememberfile, we simply display the contents to the user ③.

Otherwise, if arguments are passed to the script, we perform a case-insensitive grep to search for any matching terms in the rememberfile, and then display these results with paging as well ④.

# Running the Script

To use the remindme utility, first add notes, phone numbers, or anything else to the rememberfile with the remember script, as in Listing 3-3. Then search this freeform database with remindme, specifying as long or short a pattern as you’d like.