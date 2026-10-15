# at, batch—executes commands at a later time

```
at [-csm] [-f script] [-queue] time [date] [+ increment]
at -l [ job... ]
at -r job...
batch
```

at and batch read commands from standard input to be executed at a later time. at allows you to specify when the commands should be executed, whereas jobs queued with batch will execute when system load level permits. Executed commands read from stdin or a file at some later time. Unless redirected, the output is mailed to the user.

# EXAMPLE A.3

+   1. at 6:30am Dec 12 < program
+   2. at noon tomorrow < program
+   3. at 1945 pm August 9 < program
+   4. at now + 3 hours < program
+   5. at 8:30am Jan 4 < program
+   6. at -r 8388355320.a

# EXPLANATION

+   1. At 6:30 in the morning on December 12, start the job.
+   2. At noon tomorrow start the job.
+   3. At 7:45 in the evening on August 9, start the job.
+   4. In three hours start the job.
+   5. At 8:30 in the morning on January 4, start the job.
+   6. Removes previously scheduled job 8388355320.a.

# awk—pattern scanning and processing language

```
awk [ -f program-file ] [ -Fc ] [ prog ] [ parameters ] [ filename... ]
awk scans each input filename for lines that match any of a set of patterns specified in prog.
```

# EXAMPLE A.4