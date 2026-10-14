The first and last lines of the file show the beginning and ending time and date of the capture session. To stop recording the typescript, type exit at a shell prompt. By default, typescripts are saved to a file called typescript in the current directory; specify the file name as an argument.

⇒ To create a typescript of a shell session and save it to the file log.19990525, type:

```
$ script log.19990525 RET
Script started, output file is log.19990525
$ hostname RET
erie
$ apropos bash > bash.commands RET
$ exit RET
exit
Script done, output file is log.19990525
$
```

In this example, the typescript records a shell session consisting of two commands (hostname and apropos) to a file called log.19990525. The typescript looks like Figure 3-5.

```
Script started on Tue May 25 14:21:52 1999
$ hostname
erie
$ apropos bash > bash.commands
$ exit
exit
Script done on Tue May 25 14:22:30 1999
```

Figure 3-5. A typescript of a shell session.

NOTES: You won’t be happy with the output if you record a session with an interactive program such as Emacs or Vi. This is because such programs control the display; all of their screen-manipulating sequences will be saved to the typescript, where they will appear as junk characters to human eyes.

It’s possible, but usually not desirable, to run script from within another script session. This usually happens when you’ve forgotten that you are running it, and you run it again inside the current typescript, even multiple