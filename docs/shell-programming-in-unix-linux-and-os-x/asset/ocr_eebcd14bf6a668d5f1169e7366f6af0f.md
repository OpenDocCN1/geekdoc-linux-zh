# Chapter 8 'Round and Round She Goes

This process continues with successive words in the list being assigned to var and the commands in the loop body being executed until the last word in the list, word_i is assigned to var and the body of the loop executed. At that point, no words are left in the list, and execution of the for command is complete. Execution then continues with the command that immediately follows the done.

If there are n words listed after the in, the body of the loop will have been executed a total of n times when the loop has finished.

Here's a loop that will be executed three times:

```
for i in 1 2 3
do
  echo $i
```

To try it out, type this in directly at the terminal, just like any other shell command:

```
$ for i in 1 2 3
>
  echo $i
>
done
```

While the shell is waiting for the done to be typed to the for command, it keeps showing the secondary command prompt. When the user enters done, the shell proceeds to execute the loop. Because three items are listed after the in (1, 2, and 3), the body of the loop—in this case single echo command—will be executed of three times.

The first time through the loop, the first value in the list, 1 is assigned to the variable i. Then the body of the loop is executed. This displays the value of i at the terminal. Then the next word in the list, 2, is assigned to i and the echo command re-executed, showing in the display of 2 at the terminal. The third word in the list, 3, is assigned to i the third time through the loop and the echo command executed. At that point, no more words are left in the list, so execution of the for command is complete, and the shell displays the command prompt to let you know it's.

Now let's back up to Chapter 6 and recall the run program that enabled you to run a file through tbl, nroff, and lp:

```
$ cat run
tbl $1 | nroff -mm -Tlp | lp
$
```

If you wanted to run the files memo memo2 memo3 memo4, you could type the following at the terminal:

```
$ for file in memo1 memo2 memo3 memo4
do
```