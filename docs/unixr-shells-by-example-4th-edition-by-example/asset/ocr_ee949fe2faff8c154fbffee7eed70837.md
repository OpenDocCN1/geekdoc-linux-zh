# Table 11.4 Using the Esc Key and Filename Expansion

| Combination | Result |
|---|---|
| command [Esc]# | # precedes command with a #; puts it on the history list commented; command will not be executed. |
| command [Esc]_ | Underscore inserts the last word of the last command at the cursor. |
| command [Esc] 2_ | Inserts the second word of the last command at the cursor position. |
| word[Esc] * | * replaces the current word with all files matched. |
| word[Esc] \ | \ replaces the current word with the first filename that starts with the same characters; filename expansion. |
| word[Esc]= | Displays all filenames beginning with the same character as the current word and displays them in a numbered list. |

# EXAMPLE 11.20

(Press the Esc key for [Esc].

```
1 $ ls a[Esc]=
1) abc
2) abc1
3) abc122
4) abc123
5) abc2
2 $ ls a[Esc]*
1s abc abc1 abc122 abc123 abc2
abc abc1 abc122 abc123 abc2
3 $ print apples pears peaches
apples pears peaches
4 $ print [Esc]_
print peaches
peaches
5 $ print apples pears peaches plums
apples pears peaches
6 $ print [Esc]2_
print pears
pears
```

# EXPLANATION

1 By typing an a, followed by the Esc key and an equal sign (=), all files starting with an a are numbered and listed. (The numbers do not serve any special purpose.)

2 By typing an a, then the Esc key and an asterisk (*), the filenames starting with an a are displayed.