# Lab 7.2: The [[ COMMAND... ]] OPERATOR

Answer:The script prints the "is a regular file" message. Your interaction should look like the following:

```
[7014]: s721 ~/.kshrc
/home/vickery/.kshrc is a regular file.
```

```
[7015]:
```

The -e test succeeds, so the nested if is executed. Its -f test also succeeds, and the "regular file" message prints. The elif is skipped because the corresponding if (the nested if) succeeded, so the is a "directory" message does not print. Finally, the else is skipped because the first succeeded, so the "does not exist" message does not print.

Nested if statements, especially else statements, can give you a headache. Using elif instead of else ... if can reduce the pain to a dull thro.

![](bbox=[0.133, 0.335, 0.233, 0.403])

d)Explain what happens if you run this version of the script with the name of a directory as the parameter.

Answer:The script prints the "is a directory" message. Your interaction should look like the following:

```
[7015]: s721 ~/bin
/home/vickery/bin is a directory.
```

```
[7016]:
```

The -e test succeeds, so the nested if is executed. Its -f test fails, so the "regular file" message does not print. The elif is executed if (the nested if) failed, and the -d test succeeds, and the "is a directory" message does print. Finally, the else is skipped because the first succeeded, so the "does not exist" message does not print.

e) Explain what happens if you run the script with a parameter that is the name of neither a file nor a directory.

Answer:The "does not exist" message prints. Your interaction should look something like the following:

```
[7016]: s721 "A figment of your imagination"
"A figment of your imagination" does not exist.
```

```
[7017]:
```

The imaginary file name is in quotes because it contains embedded spaces. You could have used any name you wanted, provided it was not the name of a file or directory.