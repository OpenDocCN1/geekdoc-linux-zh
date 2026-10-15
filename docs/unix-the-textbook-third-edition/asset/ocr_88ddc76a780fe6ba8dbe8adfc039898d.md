# EXERCISE 14.6

Write a shell script that displays all command line arguments, shifts them to the left by two positions, and redisplays them. Show the script along with a few sample runs.

# EXERCISE 14.7

Update the shell script in Exercise 14.1 so that, after accomplishing this task, it sets the positional arguments to the output of the who | head -1 command and displays the positional arguments again.

# 14.6 COMMENTS AND PROGRAM HEADERS

You should develop the habit of putting comments in your programs to describe the purpose of a particular series of commands. At times, you should even briefly describe the purpose of a variable or assignment statement. Also, you should use a program header for every shell script that you write. These are simply good software engineering practices. A program header is a set of introductory comments used to explain the script. Program header and in-code comments help a programmer who has been assigned the task of maintaining (i.e., modifying or enhancing) your code to understand it quickly. They also help you understand your own code, in particular, if you reread it after some period of time. Long ago, putting comments in the program code or creating separate documentation for programs was not a common practice. Such programs when inherited by a programmer or a team are very difficult to understand and maintain, and are commonly known as legacy code. You may find different definitions for legacy code in the literature.

A good program header must contain at least the following items. In addition, you can insert any other items that you feel are important or are commonly used in your organization or group as part of its coding rules.

+   1. Name of the file containing the script
+   2. Name of the author
+   3. Date written
+   4. Date last modified
+   5. Purpose of the script (in one or two lines)
+   6. A brief description of the algorithm used to implement the solution to the problem at hand

A comment line, including every line in the program header, must start with the number sign (#), as in.

```
# This is a comment line.
```