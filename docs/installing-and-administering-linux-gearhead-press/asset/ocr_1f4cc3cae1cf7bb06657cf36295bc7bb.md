```
var2=$LOGNAME
export var1 var2
<Esc> (to leave Insert mode)
:xx<Enter> (to save sc2 and quit vi)
```

14. Make sc2 executable and run the program.

```
$ chmod 700 sc2<Enter>
$ sc2<Enter>
```

When the script has finished, examine the values of the var1 and var2 variables.

```
$ echo $var1 $var2<Enter>
```

What values do var1 and var2 have? Why?

15. Run the sc2 program again, this time by forcing it to run in the current shell.

```
$ . sc2<Enter>
```

When it is finished, check the values for var1 and var2.

```
$ echo $var1 $var2<Enter>
```

What values do var1 and var2 have now? Why?

16. Execute the ls -R / > outfile 2> errfile<Enter> command in the foreground.

```
$ ls -R / > outfile 2> errfile<Enter>
```

17. Suspend the job you just started.

```
$ <Ctrl>-$
```