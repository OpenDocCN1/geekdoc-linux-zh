# Chapter 18: Writing Scripts for Graphical Desktops

Each dialog widget provides output in two forms:

+      - Using STDERR
+      - Using the exit code status

The exit code status of the dialog command determines the button selected by the user. If an OK or Yes button is selected, the dialog command returns a 0 exit status. If a Cancel or No button is selected, the dialog command returns a 1 exit status. You can use the standard $\ ?$ variable to determine which button was clicked in the dialog widget.

If a widget returns any data, such as a menu selection, the dialog command sends the data to STDERR. You can use the standard Bash shell technique of redirecting the STDERR output to another file or file descriptor:

```
dialog --inputbox "Enter your age:" 10 20 2>age.txt
```

This command redirects the text entered in the text box to the age.txt file.

The following sections look at some examples of the more common dialog widgets you'll use in your shell scripts.

# The msgbox widget

The msgbox widget is the most common type of dialog. It displays a simple message in a window and waits for the user to click an OK button before disappearing. The following format is required to use a msgbox widget:

```
dialog --msgbox text height width
```

The text parameter is any string you want to place in the window. The dialog command automatically wraps the text to fit the size of the window you create, using the height and width parameters. If you want to place a title at the top of the window, you can also use the --title parameter, along with the text of the title. Here's an example of using the msgbox widget:

```
$ dialog --title Testing --msgbox "This is a test" 10 20
```

After you enter this command, the message box appears on the screen of the terminal emulator session you're using. Figure 18.2 shows what this looks like.

If your terminal emulator supports the mouse, you can click the OK button to close the dialog. You can also use keyboard commands to simulate a click—just press the Enter key.

# The yesno widget

The yesno widget takes the msgbox widget one step further, allowing the user to answer a yes/no question displayed in the window. It produces two buttons at the bottom of the window—one for Yes and another for No. The user can switch between buttons by using the mouse, the Tab key, or the keyboard arrow keys. To select the button, the user can press either the spacebar or the Enter key.