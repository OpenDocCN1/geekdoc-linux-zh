Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.

The which if you with pAtient eArs Attend,

Two household, both alike in dignity,

:

The command used in the preceding example displays the final Standard Output to the terminal screen via the `less` command. In many cases, you might want to display the results of the pipe as well as have a saved copy in a file on the hard disk. As a result, there exists a **tee command**, which is a filter command that takes information from Standard Input and sends that information to a file, as well as to Standard Output.

To save a copy of the manipulated prologue before displaying it to the terminal screen with the `less` command, you can use the following command:

```
[root@server1 root]# cat prologue | tr a A | sort | pr -d | tee newfile | less
```

2002-05-30 09:32 Page 1

And the continuAnce of their pARENTs' rAge.

A pAir of stAr-cross'd lovers tAke their life;

Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.