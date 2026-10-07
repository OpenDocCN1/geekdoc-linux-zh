# Lab 2.2: Command Syntax

Yes, those first three lines of punctuation marks really are command names! You saw the first one, the "dot command," in Chapter 1 when you tested your ksh setup. You can try running the colon (:) command now (it's the null command and by itself, but I don't recommend trying the left-bracket ([) command because it won't work by itself. It's a command for making tests that is provided for backward compatibility with earlier versions of sh and the KornShell. You will learn how to make tests with the KornShell in Chapter 6, "Control Structures."

The last line is the prompt from more, telling you it is waiting for you to press Space to see the next onscreen or q to quit.

Now, run the following command:

```
builtin | wc
```

+   c) What are the results? What do you think they mean?
Answer:You should see three numbers, the first two of which are the same, like this:
$ builtin | wc
61 61 397
$

They represent the number of lines and the number of words output by the builtin command.They are the same because builtin outputs one word per line.The third number is the number of characters in the output of the builtin command.

The wc (or word) command counts the number of words, lines, and characters in a file and prints them out. So, for the output shown, there were 61 lines and 61 words (because there was one word on each line), and a total of 397 characters output by the builtin command; which includes the letters in the words as well as any spaces and end-of-line characters.

+   d) How many built-in commands does the shell recognize on your system?
Answer:Your answer may vary, but the output from the last question shows that there are 61 built-in commands ksh recognizes.

The sample output was generated on a system running U/WIN Windows NT. The same command run on a SparcStation running Solaris showed 62 commands. The difference is the newgrp command,