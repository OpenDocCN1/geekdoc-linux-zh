```
~m messages      Read in messages, right-shifted by a tab
~p               Print the message buffer
~q,~Q            Quit, save letter in $HOME/dead.letter
~r,^< file       Read a file into the message buffer
~r,^< !command   Read output from command into message
~R               Mark message for return receipt
~s subject       Set subject
~t users         Add users to To list
~v               Invoke display editor on message
~w file          Write message onto file (no header)
~x               Quit, do not save letter
~!command        Run a shell command
~|,^ command     Pipe the message through the command
~:;_ command     Execute regular mailx command
~.               end of input
~?               print this help message
----------------
-
```

The most important ones to remember are ~v, to start vi with the message as entered to that point in the edit buffer; ~r, to include the contents of a file; ~h, to edit the message headers; ~!, to invoke a shell command; and ~p, to show the message that’s been entered so far:

Click here to view code image

```
I wanted to wish you a cheery good morning!  You asked about
the contents of that one file, so here it is:
~!ls
Archives/        bin/            deleteme        sample
InfoWorld/       buckaroo        dickens.note    sample2
Mail/            buckaroo.confused keylime.pie     src/
News/            cheryl          mbox            temp/
OWL/             csh.man         newsample
awk script       dead.letter     owl.c
!
```

The output of the command isn’t included in the message, but is shown on screen if you use the ~p command:

Click here to view code image

```
~p
---
Message contains:
To: dunlap
Subject: Good morning!

I wanted to wish you a cheery good morning!  You asked about
the contents of that one file, so here it is:
(continue)
-
```

# 4. To read in a file, use the ~r command:

```
~r dickens.note
"dickens.note" 28/1123
```

Here, the contents of the file are included in the note, but mailx didn’t list the contents to the screen. Again, using ~p lists the current message: