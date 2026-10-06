# 60 Part I ♦ SUSE Linux Basics

it. The name less command comes from the fact that it originally began as an open source version of the more command (and before more itself became an open source command) and because it originally did less than the more command (the author had a sense of humor). Nowadays, the less command has added many features, including the fact that you can use keyboard shortcuts as pressing the letter b when viewing a file to move backward through the file. The main page of less lists all the hot keys that can be used for navigating through a file while reading it less. Both more and less use the hot q to quit.

+   * more /etc/passwd—Views the contents of /etc/passwd
* less /etc/passwd—Views the contents of /etc/passwd

# Viewing the Start or End of Files

The head and tail commands allow you to see a specific number of lines from the top or bottom of a file. The tail command has the very useful feature that you can use tail -f to keep an eye on a file as it grows. This is particularly useful for watching what is being written to a log when you make changes in the system. Consider the following examples:

+   * head -n5 /etc/passwd—Prints the first five lines of /etc/passwd to the screen
* tail -n5 /etc/passwd—Prints the last five lines of /etc/passwd to the screen
* tail -f /var/log/messages—Views the last few lines of /var/log/messages and continues to display changes to the end of the file in real time

# Searching Files with grep

The grep (global regular expression print) command is a very useful tool for finding stuff in files. It can do much more than the examples follow that this pattern graph indicate. Beyond simply searching for text, it can search for regular expressions, and regular expressions are a subject for a book in themselves.

When administering a system, you often need to look for lines in a file that contain a string. In the first example follows, you simply find the lines in the file that contain the string bible. The examples with tail are examples of piping the output from one command to another: very powerful concept that was also introduced in the section “Advanced Shell Features,” earlier in this chapter. In the first case, you get the output from the tail command, and you just select the lines that contain 404. In the second, select the lines that do not include the string googlebot; the -v option indicates “not.” In the example, the “symbol represents the start of a line, so you see only the lines that do not start with the