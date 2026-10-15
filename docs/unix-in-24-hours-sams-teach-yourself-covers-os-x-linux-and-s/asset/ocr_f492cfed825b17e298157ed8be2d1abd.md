more commands than are shown in this initial task, too, so further study is helpful.

# Task 20.2: Sending Mail from the Command Line

Now you know how to read your electronic mail using Berkeley Mail (mailx), and you know how to send mail from within the program. How do you send messages and files to people from the command line? It’s quite simple. You even can specify the message subject with the -s starting flag.

+   1. To send a message to someone, enter the name of the command followed by the recipient’s account name:

Click here to view code image

```
$ mail marv
Subject: Interested in lunch tomorrow?
-
I now can enter as many lines of information as I want, ending, as within the Berkeley Mail program itself, with either ^d (call this “Control-D” to sound like a Unix old-timer) or . on a line by itself:
```

Click here to view code image

```
I’m going to be in town tomorrow and would like to rustle up some Chinese food. What’s your schedule look like?

Dave
.
Cc: _
```

Again, I’m offered the option of copying someone else, but—again—I opt not to do so. Pressing Return sends the message.

+   2. To send a file to someone, combine file redirection with the use of the -s flag:

Click here to view code image

```
$ mail -s “here’s the contents of sample.file” marv < sample.file
```

The file was sent without any fuss.

+   3. Even though mailx gives you no indication, several commands are available for use while you’re entering the text of a message, and all can be listed with ~?:

Click here to view code image

```
$ mail dunlap
Subject: Good morning!
~?
-------- ~ ESCAPES --------
~~          Quote a single tilde
~a,~A       Autograph (insert ‘sign’,‘Sign’ variable)
~b users    Add users to Bcc list
~c users    Add users to Cc list
~d          Read in dead.letter file
~e          Edit the message buffer
~f messages Read in messages, do not right-shift
~h          Prompt for Subject and To, Cc and Bcc lists
~i variable Insert variable into message (~a := ~i sign)
```