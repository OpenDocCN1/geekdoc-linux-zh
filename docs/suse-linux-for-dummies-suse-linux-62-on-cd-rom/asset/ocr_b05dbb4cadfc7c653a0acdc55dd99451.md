# 176 Part III: Using Linux

The pipe symbol |, takes the output of the cut command and feeds it the sed command. Look at the part of the command line to the right of the pipe symbol and you can see that the -e option of the sed command tells the command to use the next string of characters (in this case, what between the two apostrophes, or single quotation marks) as a command for the sed stream editor.(The command here is basically the same as the s command in the ed and ex editors, which you can read about Chapter 9). The command finds strings of characters between the first and second slash marks and replaces them with the characters between the second and third marks.

Note the quotation marks around '/s/:/ - /. This makes the shell think of the entire string of characters as one thing, and presents the string to the sed editor as the thing that - has to work with. Without the single quotation marks, the shell should include the blanks in the string that three different things are in that string of characters: s://-, and /. In state-ments, unquoted blank space (called white space) is considered a separator.

![](bbox=[0.08, 0.395, 0.215, 0.565])

Continuing with your report, you want some type of header that states the subject of the report and the date. You can use the echo command (for the header) and the date command (for the date):

```
echo Report of login names and users on the Linux system
date
echo ============================
cut -f 1,5 -d: /etc/passwd | sed -e 's/:/ -/
```

These four lines are not difficult to type, but you would have to remember them and retype each time you run the report. If you like to save time whenever we can, and our memory cells seem to be dropping like... ah, we forget. For those reasons, we want to use our favorite text editor to type the lines in a file.

![](bbox=[0.12, 0.685, 0.215, 0.805])

Our favorite editor is vi. If you want to use another editor, we won't stop you. But be sure to name your file quagmire so that the rest of the example will work.

In the following, we're using vi to edit a file named quagmire, entering the commands before into that file:

```
maddog@localhost:~ > vi quagmire
a
echo Report of login names and users on the Linux system
date
echo ============================
cut -f 1,5 -d: /etc/passwd | sed -e 's/:/ - /
<ESC>
wq:
```