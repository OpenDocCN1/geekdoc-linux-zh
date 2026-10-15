If you would load the file shown in Listing A.15 with the command :so <file-name>, then you would be able to create a while loop by inputting the string WLOOP. The same goes for FORI; this abbreviation creates a for loop with the variable i as counter. To include the Enter key in the abbreviation, you have to input the key combination Ctrl-V followed by the Enter key. Using this system is a matter of taste, though. If you have the feeling the system speeds things up considerably, then you should use it or at least give it a try.

# A.4.5 Joining Lines

If you need to join two consecutive lines in vi, you could use the command J. You would have to position the cursor on the first of the two lines to be joined and press J to join them into one single line. Listing A.16 shows an example.

# LISTING A.16 Joining Lines in vi

```
This is a line
split in two.

Another line.
```

If you would position the cursor in the first line and type j in command mode, the two lines would look like so:

```
This is a line split in two.

Another line.
```

This command seems to answer one of the more frequently asked questions regarding vi.

# A.4.6 A Short Table with Important vi Commands

To close the hints regarding vi, a short—and by no means complete—table (Table A.1) of useful commands follows for easy reference.