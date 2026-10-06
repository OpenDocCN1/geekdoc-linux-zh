# Regular Expressions

Regular expressions are used in programming and in some Linux shell process. They provide us easiness in many areas. They often us e forgot the information we need from such kinda, control of user input, etc.. For example, while searching an given template is an easy job, we need to use regular expressions to get the search complex and large files. They are not only beneficial in the search process, also we can use them for operations to be applied to search procedures.

Now let's explain some of the regular expressions used by a Linux system and do a few examples:

+   - Character in the square brackets indicates the desired template to use. For example, to list the phrases beginning with A, and h or l in users.txt file, we use grep A[hl] users.txt command.

```
root@kemal:~# cat users.txt
Ali
Ahmet
Aslan
Mehmet
Zeynep
root@kemal:~# grep A[hl] users.txt
Ali
Ahmet
root@kemal:~# _
```

To find the phrases starts with A and continue with a character between a-z, we can use grep A[a-z] users.txt command.

```
root@kemal:~# grep A[a-z] users.txt
Ali
Ahmet
Aslan
root@kemal:~# _
```