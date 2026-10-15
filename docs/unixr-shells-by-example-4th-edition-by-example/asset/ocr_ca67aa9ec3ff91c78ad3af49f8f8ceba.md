# Table 13.7 Substitution and History (continued)

| Event Designator | Meaning |
|---|---|
| ^old^new | In last history command, substitutes old string with new string. |
| command !N:w | Executes current command appending an argument (!n) from the Nth previous command. !n is a number starting at 0, 1, 2, ... designating the number of the word from the previous command, word 0 is the command itself, and 1 is its first argument, etc. (See Example 11.32.) |

# EXAMPLE 13.32

```
1  $ date
Mon Jul 12 12:27:35 PST 2004

2  $ !!
date
Mon Jul 12 12:28:25 PST 2004

3  $ !106
date
Mon Jul 12 12:29:26 PST 2004

4  $ !d
date
Mon Jul 12 12:30:09 PST 2004

5  $ dare
dare: Command not found.

6  $ ^r^t
date
Mon Jul 12 12:33:25 PST 2004
```

# EXPLANATION

+   1. The UNIX/Linux date command is executed at the command line. The history list is updated. This is the last command on the list.
+   2. The !! (bang bang) gets the last command from the history list; the command is re-executed.
+   3. Command number 106 from the history list is re-executed.
+   4. The last command on the history list that started with the letter d is re-executed.
+   5. The command is mistyped. It should be date, not dare.
+   6. The carets are used to substitute letters from the last command on the history list. The first occurrence of an r is replaced with a t; that is, dare becomes date.