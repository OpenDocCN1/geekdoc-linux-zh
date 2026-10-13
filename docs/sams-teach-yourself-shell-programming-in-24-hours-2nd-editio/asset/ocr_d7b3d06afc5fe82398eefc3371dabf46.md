which is what we want. Notice that when we added the second s command, we changed from the single command form for sed to the multiple command form that uses the -e option.

# Summary

In this chapter, we looked at filtering text using regular expressions. Some of the major topics covered were

+   - Matching characters
+   - Specifying sets of characters
+   - Anchoring expressions
+   - Escaping meta-characters

We also looked at the similarities between awk and sed and covered the use of sed in detail.

In the next chapter, I will introduce the awk command and its programming language. Using the material covered in this chapter, you will be able to use awk to perform difficult text manipulations.

# Questions

1. Using sed, write a shell function that searches for a word or simple expression in a list of files, printing out a list of matches. You do not have to support all possible sed expressions. Your function should take the word to look for as its first argument. It should treat its other arguments as a list of files.
HINT: Use double quotes (") instead of single quotes (\') to surround your sed script.

2. Write a sed command that takes as its input the output of the uptime command and prints only the load averages. The uptime command's output resembles the following:

```
$ uptime
6:34pm up 2 day(s), 49 min(s), 1 user, load average:
0.00, 0.00, 0.02
```

Your output should resemble the following:

```
load average: 0.85, 0.01, 0.03
```