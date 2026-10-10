> **Caution** Some versions of UNIX use a killall command that works differently from FreeBSD's. Specifically, this alternate killall kills all processes started by the issuing user, except those that are parents of the killall process itself. Thus, if you find yourself using a non-FreeBSD system, check the killall man page before using this command.

Both kill and killall can be used by both root and ordinary users. As you might expect, though, ordinary users are restricted to killing only their own processes.

# ## Redirection

The subject of redirection has popped up once or twice in earlier chapters. This tool is extremely important for text-based FreeBSD administration, and even for ordinary users. Redirection enables you to redirect a program's input or output, connecting it to a file rather than to the keyboard or screen.

To understand redirection, you should first understand that many text-mode programs accept input from, and send output to, multiple sources (which are often called streams). Normally, all a program's input sources are tied to the keyboard at which the user sits, and all the output sources are tied to the screen, xterm, or remote login process the user is using. The usual input and output streams are known as standard input and standard output (often abbreviated stdin and stdout, respectively). An important second output stream is known as standard error (or stderr). This secondary output source handles important error messages. Although it normally links to the same console as stdout, stderr is separate so that it may be redirected in a different way.

Redirection involves connecting these input or output streams to some other source or destination. For instance, rather than read output on your screen, you might want to direct it into a file. You can then include this file in a document you're writing with a word processor, or search through the output and study it at your leisure. You can redirect stdout by using the greater than symbol (>) and following it with the name of the file to which you want to send the output. For instance, to save a long file listing to a file, you might use this command:

```
```
$ ls -l > listing.txt
```
```

After issuing this command, you could use a paging tool such as less to view the output, load the file into a text editor, or manipulate it in any way you could manipulate any text file. Some programs tend to use stderr more than stdout, the idea being that the user should really read the "error" output immediately. Unfortunately, sometimes this output is copious, so redirecting it to a file for later perusal is often desirable. You can do so by using a minor variant of the stdout redirection: Use 2> rather than >. For