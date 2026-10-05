# 316 Part VII: Appendixices

# Synopsis

The synopsis is a shorthand way to describe what the command is looking for the way of an argument list. For example:

```
lpq [-a] [-Pprinter] [job # ...] [user ...]
```

is the synopsis for the lpq command (whose job is to show what is in the print queue). The command (lpq) is first, followed by a series of brack-eted arguments. If an argument is enclosed in square brackets, the argument is optional. That means the lpq command needs no arguments. If you type

```
[maddog@local maddog] > 1pq
```

you will probably get a no entries message, which means nothing is waiting to be printed, or a list of people's jobs is waiting to be printed on the default printer.

If you want to see what is waiting to be printed on another printer, you use the option -P followed by the name of the printer. For example:

```
[maddog@localhost maddog] > -Pzklpsa
```

Now if you type that, you probably get a message like lpq: zklpsa: unknown printer, showing that your system does not know about a printer named zklpsa. If you get something else, let me know, because that may explain why my print jobs are going ... , no, just kidding.

In any case, the purpose of this section is not to show all the functional-ity of the lpq command. Rather, the synopsis section shows in a shorthand how the command should be used, including which arguments are optional.

Another confusing thing you see is the ... notation. Looking back at the lpq command synopsis, you see it twice, once following the job # argument and once following the user argument. This notation tells you that you can list as many job numbers on the line as you want, separated by spaces, and as many user names as you want, separated by spaces.

Sometimes you see a command that begins with one hyphen (-) or two (--). These are technically known as options, whereas job # and user of the lpq command are arguments. Options tell the command how to manipulate arguments. You might see an option line that looks like this:

```
cat [-benstuvAET]
```

or even

```
ls [-abcdefghijklmnpqrstuxABCGLNQRSUX1]
```