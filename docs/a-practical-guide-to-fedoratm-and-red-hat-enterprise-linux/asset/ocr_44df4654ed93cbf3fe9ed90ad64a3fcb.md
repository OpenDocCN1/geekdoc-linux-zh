![](bbox=[0.35, 0.1, 0.65, 0.25])

Figure 27-6 An until flowchart

# until

The **until** and **while** structures are similar, differing only in the sense of the test performed at the top of the loop. Figure 27-6 shows that **until** continues to loop **until** the *test-command* returns a *true* exit status. The **while** structure loops **while** the *test-command* continues to return a *true* or nonerror condition. The **until** control structure has the following syntax:

```
until test-command
do
commands
done
```

The following script demonstrates an **until** structure that includes **read** (page 1041). When the user enters the correct string of characters, the *test-command* is satisfied and the structure passes control out of the loop.

```
```
$ cat until1
secretname=zach
name=noname
echo "Try to guess the secret name!"
echo
until [ "$name" = "$secretname" ]
do
  read -p "Your guess: " name
done
echo "Very good."
```
```
$ ./until1
Try to guess the secret name!

Your guess: helen
Your guess: barbara
Your guess: rachel
Your guess: zach
Very good
```
```