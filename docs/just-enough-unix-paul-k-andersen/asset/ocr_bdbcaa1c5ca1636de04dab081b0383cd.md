# ### 14.16  Exercises

+   1.  Find someone with an account on your computer (or on the same network) and practice using `mailx` or `Mail` to exchange messages.
+   2.  As you have seen, the s ("save") command is used inside the mail program to append a message to a file. The w ("write") command also appends messages to files. Mail yourself a message, then use the w command to put it into a file. Exit the mail program and examine the contents of the new file. What is the difference between w and s?
+   3.  The mail S ("save") command will save a mail message in a file that has the same name as the sender’s login. (If such a file already exists, the message will be appended to the file.) Try out the S command.
+   4.  The mail programs `mailx` and `Mail` make use of so-called *tilde escapes*. These are mail commands that begin with a tilde (~). You have seen how to use the tilde escape sequence `~v` to edit a message using the `vi` editor. Find out about other tilde escapes. Start up the mail program as if you were going to send a message. However, instead of typing a message, enter the tilde escape sequence `~?` (**Return**) to display a list of the tilde escapes. What do the following tilde escapes do?
+       - `~p`
+       - `~h`
+       - `~q`
+       - `~r`
+       - `~S`
+       - `~x`
+   5.  You have seen how to mail a file using the redirection operator on the command line. Thus, to send the file `myfile` to the user `fred@host`, you would type
+       ```
+       $ Mail fred@host < myfile(Return)
+       ```
+       or
+       ```
+       $ mailx fred@host < myfile(Return)
+       ```
+       When `fred` receives the message, it will not have a subject. You can remedy this using the `-s` ("subject") option, like this:
+       ```
+       $ Mail -s "This is the subject" fred@host < myfile(Return)
+       ```