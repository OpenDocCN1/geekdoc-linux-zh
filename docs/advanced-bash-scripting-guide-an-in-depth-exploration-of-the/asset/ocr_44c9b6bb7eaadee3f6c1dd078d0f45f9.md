# Advanced Bash-Scripting Guide

A lucky number is one whose individual digits add up to 7, in successive additions. For example, 62431 is a lucky number (6 + 2 + 4 + 3 + 1 = 16, 1 + 6 = 7). Find all the lucky numbers between 1000 and 10000.

# Craps

Borrowing the ASCII graphics from Example A-40, write a script that plays the well-known gambling game of craps. The script will accept bets from one or more players, roll the dice, and keep track of wins and losses, as well as of each player's bankroll.

# Tic-tac-toe

Write a script that plays the child's game of tic-tac-toe against a human player. The script will let the human choose to take the first move. The script will follow an optimal strategy, and therefore never lose. To simplify matters, you may use ASCII graphics:

```
| o | x |
|   | x |
|   | o |
```

Your move, human (row, column)?

# Alphabetizing a String

Alphabetize (in ASCII order) an arbitrary string from the command-line.

# Parsing

Parse /etc/passwd, and output its contents in nice, easy-to-read tabular format.

# Logging logins

Parse /var/log/messages to produce a nicely formatted list of user logins and login times. The script may need to run as root. (Hint: Search for the string "LOGIN.")

# Pretty-printing a Data File

Create database spreadsheets use cases with the fields separated by commas, commonly referred to as comma-separated values or CSVs. Other applications often need to parse these files.

Given a data file with comma-separated fields, of the form:

```
Jones,Bill,235 S. Williams St.,Denver,CO,80221, (303) 244-7988
Smith,404 Polk Ave., Los Angeles,CA,90003, (213) 879-5612
...
```

Reformat the data and print it to stdout in labeled, with easy-right-justify each line

# Justification

Given ASCII text input from stdin or a file, adjust the spacing to right-justify each line then send the output to stdout.

# Mailing List

Using the mail command, write a script that manages a mailing list. The script automatically e-mails the monthly newsletter, from a specified text file, and sends it to all the addresses on the mailing list, which the script reads from another file.

# Generating Passwords

Generate pseudandom 8-character passwords, using the characters in [0-9], [A-Z], [a-z]. Each password must contain at least two digits.

# Monitoring a User

You suspect that particular user on the network has been abusing her privileges and possibly attempting to hack the system. Write a script to automatically monitor and log her activities when she's signed in. The log file will save entries for the previous week, and delete those more than seven days old.

Appendix O. Exercises