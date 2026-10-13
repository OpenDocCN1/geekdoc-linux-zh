Call this script read.sh and execute it in the background as follows:

```
$ read.sh &
$
```

Because this command does not produce any output until you give it input, all you see is the command prompt. Pressing Enter at the prompt results in a message similar to the following:

```
[1] + Stopped (SIGTSTP)    read.sh &
```

This message informs you that the command read.sh is currently stopped due to the signal SIGTSTP. This signal (SIG) tells you that the program is waiting for terminal (TT) input (IN). See Chapter 19, "Signals," for more information on signals. In bash and zsh the information about the signal is not presented.

If you get a message like this, you have two choices. You can kill the process and rerun it with input redirected, or you can bring the process to the foreground, give it the input it needs, and then let it continue as a foreground or background process. This chapter explains how to handle either of these choices.

# Moving a Foreground Process to the Background

In addition to running a process in the background using &, you can move a foreground process into the background. While a foreground process runs, the shell does not process any new commands. Before you can enter any commands, you have to suspend the foreground process to get a command prompt. The suspend key on most UNIX systems is Ctrl+Z.

![](bbox=[0.22, 0.86, 0.28, 0.92])

> You can determine which key performs which function by using the stty command. By entering
> 
> $ stty -a
> 
> you are shown the following, along with a lot of other information:
> 
> intr = ^C; quit = ^\; erase = ^H; kill = ^U;
>  eof = ^D; eol = ^@; susp = ^Z;
>  eol2 = ^0; start = ^Q; stop = ^S; susp = ^Z;
>  dsusp = ^Y; reprint = ^R
>  discard = ^O; werase = ^W; lnext = ^V
> 
> The entry after susp (^Z in this example) is the key that suspends a foreground process. The character - stands for Ctrl. If Ctrl-Z does not work for you, use the stty command as shown previously to determine the key for your system.