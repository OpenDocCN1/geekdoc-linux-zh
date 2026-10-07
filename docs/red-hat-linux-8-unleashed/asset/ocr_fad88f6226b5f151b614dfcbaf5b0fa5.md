Choosing a Mail Client (MUA)

To: user1@lion.org

Subject: Issues regarding software build

Hey guy,

The software build of the project appears to be broken.
➡It is blowing up with all kinds of errors. Any ideas?

Thanks

&

If you want to respond to this message, you can type respond and press Enter. You can also type r and press Enter. By default, the command will be applied to the currently active message, which is indicated in the message list by a > (and will be the last message that you read). If you want to have the command applied to a different message, you can simply specify the message number after the command, for r2 will respond to message number 2.

A complete list of commands is available within mail by typing ? at the prompt. Note that you can abbreviate commands to the shortest abbreviation that isn't ambiguous.

# Shell Scripting with mail

As mentioned previously, mail's most useful application is its use in shell scripting. This is because the complete instruction to create and send a message can be done from the command line. For example, suppose that we have a shell script that generates a report and stores it as a file. We now want to email that file to a user at the end of the script. With mail, you could use such a command as the following:

```
$ mail user@lion.org -s "Report from shell script" < report.txt
```

-s defines a subject on the command line, and then we use shell redirection to use the file report, txt as for the message (see Chapter 22, "Shell Scripting"). It's simple, clean, and requires no user interaction to send the message.
For other options available on the main command line, see the man page for mail.

# Pine

Pine is a menu driven mail client developed by the University of Washington that was designed to be easy for new users to work with. It is similar to another client called Elm, but is easier to use. (Pine is a recursive acronym that stands for Pine is not Elm, although the University of Washington officially denies this.) Figure 19.2 shows the Pine interface.