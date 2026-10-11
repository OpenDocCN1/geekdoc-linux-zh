computer as bob. (See Chapter 20 for further information on reading e-mail). You see the message You have new mail after you enter Bob's user ID and password. You can then use the mail utility to read the mail.

# ### Passing an Argument to an E-Mail Program

You can modify how the mail utility works after you call the mail utility from a program by passing changes. The geeks call this passing an argument from the command line.

Say that you want to send a message that you keep in a file you call mysecret to your friend Bob, whose e-mail address is bob@xyz.com. You pass the mail utility mysecret and bob@xyz.com as an argument as you call the mail utility from the command line.

You can write a program that asks the user of your program to enter an e-mail address as the name of the file that contains the message to be sent to that e-mail address. Your program can then call the mail utility and pass the e-mail address and document name to the mail utility so that it can send the document.

Following is information that you can change if you call the mail utility from the command line or from within your program:

+   - The e-mail message.
+   - The destination address.
+   - The copy address.
+   - The blind-copy address.
+   - The subject.

To review how you use these features of the mail utility, see Chapter 20.

# ### Passing the e-mail message

You probably send many e-mails to your friends, so writing a program that contains the filename of the hard-coded message doesn't make too much sense, because you want to send many different messages to your friends. (Hard coding, by the way, is a geek's way of saying that you type the name of the file that contains the message as part of the program, as I do in the section "Sending E-Mail from a Program," earlier in this chapter.)