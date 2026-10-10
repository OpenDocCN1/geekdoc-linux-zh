# USING ELECTRONIC MAIL

14.2 Mailing a File

previous line. Therefore, make sure each line is correct before starting a new line:

*Don't be alarmed.* (*Return*)
*This is only a test.* (*Return*)

4  **When you finish the message, send it.** This is done by starting a new line, then pressing (*Control*-*D*) (for “done”):

(*Return*)
(*Control*-*D*)

On some systems, the computer will ask if you want to send carbon copies (Cc) to anyone:

Cc: 

5  **Send carbon copies, if any.** Enter the login name of anyone who should receive a copy of your message. If you do not intend to send carbon copies to anyone, just press (*Return*).

Cc: (*Return*)

The UNIX prompt tells you that you are back in the UNIX shell:

```
$
```

# 14.2 Mailing a File

Because the mail program has only limited editing capabilities, it is often more convenient to use the *vi* editor to create a file containing your message, then mail the file. In this section, you will see how to use e-mail to send a copy of a file.

+   1  **Create a file using the text editor.**

+   2  **Redirect the file to the e-mail program.** To send the file *poems* to the account *login*, type

```
$ mailx login < poems (*Return*)
```

or

```
$ Mail login < poems (*Return*)
```

The input redirection arrow (*<* ) tells the mail program to take its input from the contents of the file *poems*.

> WARNING  Be sure to use the input redirection arrow (*<*, not the output redirection arrow (*>*) . Using the wrong arrow can destroy the contents of the file.