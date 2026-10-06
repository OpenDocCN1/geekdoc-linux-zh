```
$ tail --bytes 6 eleven
leven
```

The final example demonstrates the -f option; following, tail tracks the output of a make command, which is being sent to the file accounts.out:

```
$ make accounts > accounts.out &
$ tail -f accounts.out
cc -c trans.c
cc -c reports.c
```

```
CONTROL-C
$
```

In the preceding example, using tail with -f has the same effect as running make in the foreground and letting its output go to the terminal; however, using tail has some advantages. First, the output of make is saved in a file. (The output would not be saved if you simply let it go to the terminal.) Also, if you decide to do something else while make is running, you can kill tail, and the terminal will be free for you to use while make continues in the background. When you are running a large job, such as compiling a large program, you can use tail with the -f option to check on its progress periodically.