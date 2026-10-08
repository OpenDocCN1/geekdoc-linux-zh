
# Advanced Bash-Scripting Guide

Write a script for a multi-user system that checks users' disk usage. If a user surpasses a preset limit (500 MB, for example) in her `/home/username/` directory, the script automatically sends her a "pigout" e-mail.

The script will use the du and mail commands. As an option, it will allow setting and enforcing quotas using the quota and setquota commands.

# Logged in User Information

For all logged users, their real names and the time and date of their last login.

Hint: use who, lastlog, and parse `/etc/passwd`.

# Safe Delete

Implement a "safe" delete command, `sdel.sh`. Filenames as command-line arguments to these are not deleted, but instead zipped if not already (use file to check), then moved to `~/TRASH` directory. Upon invocation, the script checks the `~/TRASH` directory for files over 48 hours and permanently deletes them. (An alternative might be to have a second script handle this, periodically by the cron daemon).

Extra credit: Write the script so it can handle files and directories recursively. This would give it the capability of "safely deleting" directory structures.

# Making Change

What is the most effective way to change $1.68, using only coins in circulation (up to 25c)? It's 6 quarters, a dime, and three cents.

Given any arbitrary command-line input in dollars and cents ($...), calculate the change, using the minimum number of coins. If your country is not the United States, you may use your local currency units inside. The script will need to parse the command-line input, then change it to multiples of the smallest monetary unit (cents or whatever). Hint: Example 24-8

# Quadratic Equations

Solve a quadratic equation of the form $Ax^2 + Bx + C = 0$. Have a script take as the coefficients, A, B, and C, and return the solutions to five decimal places.

Hint: pipe the coefficients to bc, using the well-known formula, $x = (-B \pm \sqrt{B^2 - 4AC}) / 2A$.

# Table of Logarithms

Using the bc printf command, print out a nicely-formatted table of natural logarithms in the interval 0.00 and 10.00, in .01.

Hint: bc requires the -1 option to load the math library.

# Unicode Table

Using Example-T as a template, write a script that prints to a file Unicode table.

Hint: Use the -e option to echo `\uXXXX`, where XXXX is the Unicode numerical designation. This version 4.2 or later of Bash.

# Sum of Matching Numbers

Find the sum of all five-digit numbers (in the range 10000 - 99999) containing exactly two out of the set of digits: { 4, 5, 6 }. These may repeat within the same number, and if so, count once for each occurrence.

Some examples of matching numbers are 42057, 76438, and 89515.

# Lucky Numbers

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

Reformat the data and print it to stdout in labeled, with easy-right-justify each line.

# Justification

Given ASCII text input from stdin or a file, adjust the spacing to right-justify each line then send the output to stdout.

# Mailing List

Using the mail command, write a script that manages a mailing list. The script will automatically e-mails the newsletter, from a specified file, and sends it to all addresses on the mailing list, which the script reads from another file.

# Generating Passwords

Generate random 8-character passwords using the characters in [0-9], [A-Z], [a-z]. Each password must contain at least two digits.

# Monitoring a User

Suspect that particular user on the network has been abusing privileges and possibly attempting to hack the system. Write a script to automatically monitor and log activities when she signs in. The log file will save entries for the previous week, and delete those more than seven days old.

# Checking for Broken Links

Using the -l option, write a script that checks for broken links. The output will be a listing of all occurrences in the target file. This exercise tests mastery of Regular Expressions.

# Square Root

Write a script to calculate square roots using Newton's Method. The algorithm for square roots, expressed as a snippet of Bash, is:

```
guess = $argument
# argument is the number to find square root of
# guess is each successive calculated trial solution.
# Our first guess is the root itself.
oldguess = 0
# oldguess is the previous guess.

tolerance = .000001
# To close a tolerance we wish to calculate.

loopcnt = 0
# Let's keep track of how many times through the loop.
# Some arguments require more iterations than others.
```

```
while [ $(ABS $oldness) -gt $tolerance ];
  # ABS is (floating point) to find the absolute value of the difference between the two terms.
  # So, as long as difference between current and previous trial solution (guess) exceeds the tolerance, looping.
  oldness=$guess # Update oldness to previous guess.

  =================================
  guess=$($guess + $argument / $oldness) / 2.0
  = 1/2 (($oldness + $argument) / $oldness)
  equivalent to:
  = 1/2 ($oldness + $argument / $oldness)
  # that is, "Averaging out" the trial solution and the proportion of argument deviation
# (in effect, splitting the error in half)
  # This converges on an accurate solution with surprisingly few loop iterations
  # for arguments > tolerance, of course.
  =================================
  ((count++)) # Update loop counter.
done
```

It's a simple recipe, and at first glance easy to convert into a working script. The problem, is, that Bash has no native support for floating point numbers. The script writer needs to use bc or awk to convert the numbers and do calculations. It could get messy

# Logging File Access

Log accesses to the files in /etc during the course of a day. This information should include the filename, username, and access time. If any alterations to the files take place, that will be flagged. We write this data as table (tab-separated) formatted records in a logfile.

# Monitoring Processes

Write a script to continuously monitor running processes and to keep track of how processes each spawn. If a process spawns more than five children, the script sends an e-mail to the system administrator (root) with all relevant information, the time, PID of the parent, PIDs of the children, etc. The script appends to a log file every ten minutes.

# Strip Comments

Strip all comments from a shell whose name is specified on the command-line. Note that the initial # line must not be stripped out.

# Strip HTML Tags

Strip all the HTML tags from a specified HTML file, reformat it into lines between 60 and 75 characters in length. Reset indent and block spacing, as appropriate, and convert HTML tables to their approximate equivalent.

# XML Conversion

Convert an XML file to both HTML and text.

Optional: a script that converts Docbook/SGML to XML.

# Chasing Spammers

Write a script that analyzes a e-mail by DNS lookups on the IP addresses in the headers to identify the relay hosts as well as the originating ISP. The script will forward the unaltered message to the responsible ISPs. Of course, it will be necessary to filter out your own ISP's IP address, so you don't end up spamming yourself.

Appendix O. Exercises
