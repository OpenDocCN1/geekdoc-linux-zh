# Exam Prep Questions

+   1. What would you call the feature of the **bash** shell that allows a string to be typed that would then call another string that contains variables and recursive actions that is contained in memory?
+   
+       ○ A. Script
+       ○ B. Alias
+       ○ C. Function
+       ○ D. Program

Answer **C** is correct because only a function has the necessary capabilities, particularly recursive actions such as looping. Answer **A** is incorrect because a script is not contained in memory; it’s on disk. Answer **B** is incorrect because an alias has most of the features but doesn’t allow recursive actions. Answer **D** is incorrect because a program is binary and exists on disk until executed.

2. Enter in the exact command string used to declare an alias named \u200b\u200b that executes the following commands:

`ps ; file *`

The correct answer is `alias \u200b\u200b='ps ; file *'`. There are no alternative correct answers.

+   3. On a Linux system installed with the default shell, you need to execute a shell script that contains variables, aliases, and functions by simply entering its name on the command line. What should be the first line of the script? (Choose all that apply.)
+   
+       □ A. Nothing
+       □ B. `/\u200b#bin/csh`
+       □ C. `/\u200b#bin/sh`
+       □ D. `exec=/\u200b#bin/bash`
+       □ E. `/\u200b#1/bin/bash`

Answers **A**, **C**, and **E** are correct because the features mentioned as being in the script are all related to the **bash** shell. Either you use answer **E** to specifically set it or you allow the default of **bash** to be used by not specifying a shell, and on a default Linux system, `/\u200b#bin/sh` is a link to `/\u200b#bin/bash`. Answer **B** is incorrect because the syntax is incorrect for the string and the **csh** shell won’t do what the question requires. Answer **D** is incorrect because the line is incorrect and means nothing in a shell script.