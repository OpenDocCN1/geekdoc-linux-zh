# Embedding Commands

Suppose you create a script that will automatically run when you log in each day. The script might, for example, print "Greetings!" onscreen and possibly deliver a cle(a)ver message: "Say, you're looking sharp today!" You could easily do this with the information you've learned so far in this chapter.

What would be handy here would be to add a line to the script that tells Unix to do all those things plus name the most recently used file—for those of you who need a reminder about what you were last working on. You could just use an ls command, but that would only list the filenames and not integrate the information with the rest of your morning greeting. Instead, a better (and more attractive) idea would be to bundle a couple of commands and use them with echo (Figure 10.4) to embed the information right into the greeting.

# To embed a command:

+   1. vi myscript
+   To begin, open myscript or another script in your favorite editor. Your script might look like Figure 10.4, with the greeting onscreen.

![](bbox=[0.58, 0.1, 0.92, 0.38])

Figure 10.4 Embedding commands just requires an additional couple of lines in the script.

# Using Clever Dates

You can use the date command to deliver any date with any format. In general, use date "+Today is %A", but you can use any or all of the following bits:

+   - %d includes the date.
+   - %y includes the two-digit year.
+   - %Y includes the four-digit year.
+   - %m includes the numeric month.
+   - %b includes an abbreviated month.
+   - %B includes the full month name.
+   - %a includes the abbreviated day of the week.
+   - %A includes the full day of the week.
+   - %R includes the time in hours and minutes.
+   - %D includes the date in month/date/year format.

Check the man pages for the remaining several dozen options.