common options: the -q option, which gives you a quick report on whether two files actually differ, and the -y option, which prints the two files side by side on the screen so that you can compare them yourself. We will also see how the sdiff command is equivalent to the diff command with the -y option.

Some other valuable options are listed in Table 9.1.

In Examples 9.12 and 9.13, we will see how diff provides a sort of coded output as well as verbatim copies of some lines from the compared files. The codes diff provides are a mix of numbers and letters. The numbers refer to the line numbers in each file. Also, in Table 9.2, we list and explain the letter codes that diff provides. The diff command, its options, and its output codes might seem a bit complicated at first. But with practice, they are easy to grasp and make valuable analytical tools.

# **Example 9.12 Comparing Files with diff**

Don Quixote has suggested that Sancho read and review a number of books if he (Sancho) is to accompany the Don on his noble and chivalrous

# **Table 9.1 Selected diff Options**

| OPTIONS | DESCRIPTION |
| :--- | :--- |
| -b | Ignore leading, repeating, end-of-line spaces, tab characters, and so on. |
| -e | Print a text editor script that you might use to modify the first file so that it would be identical to the second file. |
| -w n | For two-column output, the total number of characters used for both columns must have a maximum n characters. (The default is 130 characters, but most users prefer to set it to 80 or so.) |

# **Table 9.2 diff Output Codes**

| CODE | DESCRIPTION |
| :--- | :--- |
| a | Add or append lines to the first file to obtain the result shown in the second file. |
| c | Lines that have been changed between the first and second file |
| d | Lines deleted from the second file. (Although Example 9.12 did not include a d, its meaning is reasonably straightforward.) |