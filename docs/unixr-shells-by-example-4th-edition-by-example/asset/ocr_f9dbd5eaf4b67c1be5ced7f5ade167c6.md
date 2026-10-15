# EXPLANATION

+   1 These examples demonstrate an n-type completion. If the word in the first set of forward slashes is typed (the current word) and matched, the next word (in the second set of forward slashes) will be completed according to the word type. The complete command lists two n-type completions, one for the rm command and one for the find command. When the rm command is executed with the -r switch, the word following -r must be of type directory if completion is to be performed. The rule for the find command is: if the -exec option is given, any words following it must be commands if completion is to be performed.
+   2 The output of the ls command shows that testing is a directory.
+   3 Filename completion is successful for the rm command because word completion is attempted for a directory named testing. If testing were a plain file, the completion would not have been performed.

# 9.16 TC Shell Spelling Correction

Spelling correction, a feature added to the TC shell, is the ability to correct spelling errors in filenames, commands, and variables. If using the emacs built-in editor, the spelling error can be corrected by using the spelling correction keys, bound to the Meta-s or Meta-S keys (use the Alt or Esc key if you don’t have Meta, and Meta-S to correct an entire line. The value of the prompt, prompt3, displays the spelling correction prompt. If you are using the vi built-in editor, set the built-in variable correct, and the shell will prompt you to fix the spelling.

# Table 9.18 The correct Variable Arguments

| Argument | What It Does |
|---|---|
| all | Spell-corrects entire command line |
| cmd | Spell-corrects commands |
| complete | Completes commands |

# EXAMPLE 9.93

```
1 > finger[Alt-s]  # Replaces finger with finger
2 > set correct=all
3 > dite
CORRECT?date (y/n/e/a)? yes
Wed Aug 8 19:26:27 PDT 2004
```

> 7 From the tsch man page: "Beware: Spelling correction is not guaranteed to work the way one intends, and is provided as an experimental feature. Suggestions and improvements are welcome."