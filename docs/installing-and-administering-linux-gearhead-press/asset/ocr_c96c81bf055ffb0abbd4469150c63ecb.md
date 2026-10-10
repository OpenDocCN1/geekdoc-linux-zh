Thus, the shell still does wildcard expansion, but the expansion goes to only one character instead of from zero to any number of characters. As with the asterisk wildcard, the exception is that matches will not occur to files beginning with a dot (.). Example 7.8 illustrates the exception. From our experience with the asterisk wildcard, we could predict quite naturally that there would be an "exceptions to the exception" here, too. A match will be made to a single dot string if the single dot is included as part of the search string. Example 7.9 illustrates this situation.

# Example 7.7 The Question Mark (?) Wildcard

Juana has found another way to list her telephone list files. She goes to her /home/gutieju/admin/phone\*s subdirectory and enters

```
$ ls RFI_Tel\*<Enter>
RFI_Tel1 RFI_Tel2 RFI_Tel3
```

Still looking for a technique that would yield faster typing, she tries

```
$ ls ??? ????\*<Enter>
RFI_Tel1 RFI_Tel2 RFI_Tel3
```

# Example 7.8 An Exception to the Question Mark (*) Wildcard Expansion

Perez wants to check his operating environment. To list his hidden .bash files, located in his home directory, he mistakenly enters

```
$ echo ?bash\* <Enter>
?bash\*
```

This time, it does not really surprise him that the shell just echoes his input back to the screen and does not list any files. But instead of calling Freston, he recalls what happened with the asterisk exceptions and perseveres on his own. See Example 7.9.

# Example 7.9 An Exception to the Exception to the Question Mark (*) Wildcard Expansion

Perez, remembering what happened when he was working with the asterisk wildcard, enters the following in his home directory:

```
$ echo .bash_??????\*<Enter>
.bash_history .bash_profile
```