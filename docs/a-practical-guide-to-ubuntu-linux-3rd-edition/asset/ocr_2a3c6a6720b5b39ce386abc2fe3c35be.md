![](bbox=[0.37, 0.09, 0.79, 0.31])

Figure 27-5 A while flowchart

executes the commands between the do and done statements. See page 955 for information on the test builtin.

```
```
$ cat count
#!/bin/bash
number=0
while [ "$number" -lt 10 ]
do
    echo -n "$number"
    ((number +=1))
done

echo
$ ./count
0123456789
$
```
```

The echo command following do displays number. The -n prevents echo from issuing a NEWLINE following its output. The next command uses arithmetic evaluation $((...)); page 1016] to increment the value of number by 1. The done statement terminates the loop and returns control to the while statement to start the loop over again. The final echo causes count to send a NEWLINE character to standard output, so the next prompt occurs in the leftmost column on the display (rather than immediately following 9).

# **optional The spell_check SCRIPT**

The aspell utility checks the words in a file against a dictionary of correctly spelled words. With the list command, aspell runs in list mode: Input comes from standard input and aspell sends each potentially misspelled word to standard output. The following command produces a list of possible misspellings in the file letter.txt:

```
```
$ aspell list < letter.txt
quickly
portible
frendly
```
```