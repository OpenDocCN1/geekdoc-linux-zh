# ## The inputbox widget

The inputbox widget provides a simple text box area for the user to enter a text string. The dialog command sends the value of the text string to STDERR. You must redirect that to retrieve the answer. Figure 18.4 shows what the inputbox widget looks like.

![](bbox=[0.34, 0.27, 0.76, 0.55])

As you can see in Figure 18.4, the inputbox provides two buttons—OK and Cancel. If the Cancel button is clicked, the exit status of the command is 1; otherwise, the exit status is 0:

```
```
$ dialog --inputbox "Enter your age:" 10 20 2>age.txt
$ echo $?
0
$ cat age.txt
125
```
```

You’ll notice that when you use the cat command to display the contents of the text file, there’s no newline character after the value. This way, you can easily redirect the file contents to a variable in a shell script to extract the string entered by the user.

# ## The textbox widget

The textbox widget is a great way to display lots of information in a window. It produces a scrollable window containing the text from a file specified in the parameters:

```
```
$ dialog --textbox /etc/passwd 15 45
```
```

The contents of the /etc/passwd file are shown within the scrollable text window, as illustrated in Figure 18.5.