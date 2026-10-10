# USING DBX

F.7 Tracing Variables and Functions

```
(dbx) run (Return)
```

dbx will run the program, displaying the values of the variables and showing calls to the function:

```
Running: a.out
(process id 3558)
main called from function _start
initially (at line "recip.c":8): recip = -26843620
initially (at line "recip.c":8): n = 0
This program computes reciprocals.
Enter a number:
```

Enter the number 1 at the prompt and note how the values of the variables are printed as they change:

```
Enter a number: 1 (Return)
after line "recip.c":10: n = 1
after line "recip.c":11: recip = 1
The reciprocal of 1 is 1.
main returns 1

execution completed, exit code is 1
```

Enter the rerun command:

```
(dbx) rerun (Return)
```

dbx will run the program again:

```
Running: a.out
(process id 3565)
main called from function _start
initially (at line "recip.c":8): recip = -26843620
initially (at line "recip.c":8): n = 0
This program computes reciprocals.
Enter a number:

Enter zero to cause an error:
```

```
Enter a number: 0 (Return)
terminating signal 8 SIGFPE
```

Leave dbx:

```
(dbx) quit (Return)
```

Use the ls command to see that a core file was created:

```
$ ls (Return)
```