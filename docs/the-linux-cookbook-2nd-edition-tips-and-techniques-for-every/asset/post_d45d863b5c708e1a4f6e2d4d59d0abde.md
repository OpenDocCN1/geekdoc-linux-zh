
possible value to the last possible value of the field, inclusive. Time and date fields may also contain ranges of numbers, and individual numbers may be given separated by commas.

To write comments in your crontab file, begin a lines with a hash sign (#); the line will be ignored by the system. Blank lines are also ignored.

For example, a simple crontab file might look like Figure 28-1.

```
# This is my sample crontab file.

# Runs the 'foo' command at noon every single day.
0 12 * * * foo

# Runs the 'bar' command at 1:23 in the morning on every day in June.
23 1 * Jun * bar

# Runs the 'foobar' command at half-past four and five p.m. every Monday
# through Wednesday whose day of the month is between 1 and 14.
30 16,17 1-14 * Mon-Wed foobar
```

Figure 28-1. A simple crontab file.

The following recipes show how to manage CRON jobs.

## 28.3.1 Adding a CRON Job

To add or change a CRON job, make the appropriate changes to your crontab file, and then run crontab with the name of this file as an argument. This command replaces your existing CRON table with the one contained in your crontab file.

⇒ To add a new CRON job contained in your crontab file cron.txt, type:

```
$ crontab cron.txt [RET]
```

## 28.3.2 Removing a CRON Job

You remove jobs from CRON by removing your CRON table. Do this by running crontab with the -r option.

⇒ To remove your CRON table, type:

```
$ crontab -r [RET]
```

NOTES: To remove only some of your CRON jobs, or to change your CRON jobs, just revise your crontab file, deleting or revising the entries you want to, and then add your CRON table (as described in the previous recipe).

## 28.3.3 Listing Your CRON Jobs

To list all of the CRON jobs you have scheduled, use crontab with the -l option.

⇒ To list your CRON jobs, type:

```
$ crontab -l [RET]
```

## 28.4 Watching a Command from Time to Time

Use watch to observe the output of a command and watch it run from time to time. It runs the command you give as an argument, repeatedly, every two seconds, until it is interrupted. Each time the command is run, the display is updated with the new results. This is particularly useful for when you want to closely watch some files in a directory and note the changes as they occur.

⇒ To watch the detailed contents of the current directory, type:

```
$ watch ls -l [RET]
```

This command will display the contents of the current directory in the terminal you run it in, and it will continually update every two seconds. To change the interval, give it as an argument to the -n option.

⇒ To watch the detailed contents of the current directory, updating by the second, type:

```
$ watch -n 1 ls -l [RET]
```

Use the -d flag to highlight the differences in the updates.

⇒ To watch the detailed contents of the current directory, updating every ten seconds, and highlighting all the differences, type:

```
$ watch -d -n 10 ls -l [RET]
```

NOTES: Sometimes you might find it nice to run your watch session in a little xterm of its own. If you're not in X, you might want to devote a console terminal to it.

## 29. Mathematics

Tools and techniques for dealing with numbers are the subject of this chapter: listing them in sequence or randomly, calculating arithmetic, cryptography, and converting between units. Larger applications, such as spreadsheets and plotting tools, are also mentioned.

## 29.1 Calculating Arithmetic

As you might expect, there are many tools for making arithmetic calculations in Linux. The following recipes describe how to use two of them for two common scenarios; a list of other calculator tools, including a visual calculator, appears at the end of this chapter (see Recipe 29.9 [Using Other Mathematics Tools], page 579).

## 29.1.1 Making a Quick Arithmetic Calculation

To do a quick calculation that requires only addition, subtraction, multiplication, or division, you can use Bash's built-in arithmetic evaluation feature to perform the calculation right at the shell prompt. It makes it even easier if you make a shell script named calc, as in Figure 29-1.

```
#!/bin/sh
echo $(( expression = $ ))
```

Figure 29-1. The calc script.

Once you install this script (see Recipe A.3.4 [Installing a Shell Script], page 708), you can use it at the shell prompt to get the results of any simple arithmetic calculation.

To do this, give the expression to evaluate as an argument to calc. Use an asterisk (*) for a multiplication sign and a forward slash (/) for division; to output the remainder, use a percent sign (%) instead of a slash. You can use parentheses to group expressions—but when you do, be sure to quote them (see Recipe 3.1.3 [Quoting Reserved Characters], page 56).
