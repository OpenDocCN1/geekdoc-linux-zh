
[content]
# Discussion

When aspell finds a misspelled word, it writes the word to standard output when the action is list. When the action is check, aspell displays a screen of information and waits for your instructions. This screen allows you to control what aspell does with the word and includes information to help you. The top line of the screen shows the potentially misspelled word. If similar words are in the dictionary, they are given in a numbered list. You can enter one of the numbers to select a word in this list, or you can enter another command. The commands available in interactive mode are listed in Table III-1.

| Command | Table III-1 Description |
| --- | --- |
| SPACE | Takes no action and goes to next misspelled word. |
| number | Selects suggested word number to replace the misspelled word. |
| r or R | Replaces the misspelled word with the word that you enter at the bottom of the screen. R replaces all occurrences of this word, whereas r replaces this occurrence only. |
| a | Adds the word to your personal dictionary. |
| i or l | Ignores the word: the same as SPACE. I ignores all occurrences of this word, whereas i ignores this occurrence only. |
| x | Saves the file as corrected so far and exits from aspell. |

The items in Table III-1 appear in a menu at the bottom of the screen. In the middle of the screen is the input line containing the potentially misspelled word (highlighted) with a few lines of context. See the “Examples,”

# Notes

The aspell utility is not a foolproof way of finding spelling errors. It also does not check for misused but properly spelled words (such as red instead of read).

# Examples

The following examples use aspell to correct the spelling in the memo.txt file:

```
$ cat memo.txt
Here's a document for teh aspell utilitey
to check. It obviously needs proofing
quiet badly.
```

The first example uses aspell with the check action and no options. The appearance of the screen for the first misspelled word, teh, is shown. At the bottom of the screen is the menu of commands that can be given at this point. The nine numbered words all differ slightly from the misspelled word:

$ aspell check memo.txt
Here's a document for teh aspell util utily
to check. It obviously needs proofing
quiet badly.

+   1) the 6) th
2) Te 7) tea
3) tech 8) tee
4) Th 9) Ted
5) eh 0) tel
i) Ignore I Ignore all
r) Replace R) Replace all
a) Add x) Exit

?
The next example uses the list action to display a list of misspelled words. The word quiet is not in the list—it is not properly used but is properly spelled:

$ aspell list < memo.txt
teh
aspell
utilitey
obviously

The last example also uses the uses list action. It shows a quick way to check the spelling of a word or two with a single command. The user gives the aspell list command then enters separate temperature into aspell's input (the keyboard). After the user enters RETURN and CONTROL-D (to mark the end of file), aspell writes the misspelled word to standard output (the screen):

$ aspell list
seperate temperature
CONTROL-D
seperate

# at

Executes a shell script at a time you specify

-   at [options] time [date] [+increment]
atq
atrm job-list
batch [options] [time]

The utility executes commands it receives from standard input as a shell script in the working directory at the time you specify. When at cancels commands, it sends you the resulting output and standard error via e-mail. You can redirect the output to avoid getting mail.

The atq utility displays a list of jobs you have queued. Normally atq displays all the jobs that you have scheduled on the system. When you run atq as Superuser, it displays all the at jobs scheduled by all users. The atrm utility cancels jobs that you have queued. The batch utility schedules jobs so they run when the CPU load on your system is low (that is, when it is not too busy).

# Arguments

The time is the time of day you want to execute the job. You can specify the time as a one-, two-, or four-digit number. One- and two-digit numbers specify an hour, and four-digit numbers specify an hour and minute. You can also give the time in the form hh:mm. The utility assumes a 24-hour clock unless you place am or pm immediately after the number, midnight, noon, or teatime (4:00 P.M.) in place of time.

The date is the day of the week or date of the month on which you want to execute the job. When you do not specify a day, at executes the job today if the hour you specify is greater than the current hour. If the hour is less than the current hour, at executes the job tomorrow.

Specify a day of the week by spelling it out or abbreviating it to three letters. You can also use the words today and tomorrow.

Use the name of a month followed by the number of the day in the month to specify a date. You can follow the month and day with a year.

The increment is a number followed by one of the following (plural or singular allowed): minutes, hours, days, or weeks. The utility adds the increment to the time you specify. You cannot give an increment if you have already given a date.

When using atrm, job-list is a list of one or more job numbers for jobs. You can identify job numbers by using with the -l option or by using atq.

# Options

The -l and -d options are not for when you initiate a job with at. You can use them only to determine the status of a job or to cancel a job. The -f and -m options work with and at batch, not with atq or atrm.

-   -d delete jobs that you previously submitted with at. The job-list argument is a list of one or more job numbers of the jobs you want to cancel. If you do not remember the job number, use the -l option to list your jobs and numbers. Using this option with at is the same as running atrm.

-   -f file typing commands for at the keyboard is risky because it is difficult to correct mistakes. This option gives the name of a file that contains a shell script you want to execute at the specified time

-   -l list displays a list of all jobs that you have submitted with at. This option with at is the same as running atq.

-   -m mail sends mail after a job is run, even when nothing is sent to standard output or standard error.

# Notes

The aspell utility is not a foolproof way of finding spelling errors. It also does not check for misused but properly spelled words (such as red instead of read).

The aspell utility is not a foolproof way of finding spelling errors. It also does not check for misused but properly spelled words (such as red instead of read).

The aspell utility is not a foolproof way of finding spelling errors. It also does not check for misused but properly spelled words (such as red instead of read).

The aspell utility is not a foolproof way of finding spelling errors. It also does not check for misused but properly spelled words (such as red instead of read).

# Examples

The following examples use aspell to correct the spelling in the memo.txt file:

The following examples use aspell to correct the spelling in the memo.txt file:

$ cat memo.txt
Here's a document for teh aspell utilitey
to check. It obviously needs proofing
quiet badly.

The first example uses aspell with the check action and no options. The appearance of the screen for the first misspelled word, teh, is shown. At the bottom of the screen is the menu of commands that can be given at this point. The nine numbered words all differ slightly from the misspelled word:

$ aspell check memo.txt
Here's a document for teh aspell utilitey
to check. It obviously needs proofing
quiet badly.

+   1) the 6) th
2) Te 7) tea
3) tech 8) tee
4) Th 9) Ted
5) eh 0) tel
i) Ignore I Ignore all
r) Replace R) Replace all
a) Add x) Exit

?
The next example uses the list action to display a list of misspelled words. The word quiet is not in the list—it is not properly used but is properly spelled:

$ aspell list < memo.txt
teh
aspell
utilitey
obviously

The last example also uses the uses list action. It shows a quick way to check the spelling of a word or two with a single command. The user gives the aspell list command then enters separate temperature into aspell's input (the keyboard). After the user enters RETURN and CONTROL-D (to mark the end of file), aspell writes the misspelled word to standard output (the screen):

$ aspell list
seperate temperature
CONTROL-D
seperate
