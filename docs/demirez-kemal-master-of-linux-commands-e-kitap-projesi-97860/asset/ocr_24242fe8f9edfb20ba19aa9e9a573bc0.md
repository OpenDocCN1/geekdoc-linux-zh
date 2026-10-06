```
root@kemal:~zeyno# tr a-z A-Z < LISTA > NEW_LISTA
root@kemal:~zeyno# cat NEW_LISTA
AHMET
MEHMET
ALI
VELI
ZEYNO
root@kemal:~zeyno# _
```

With our command, we got LIST file as input, created NEW_LISTA file by lowercase letters in uppercase in the text and we write in the file. If we use the tr command with d, the specified character will be ignored. For example, when we use cat LISTA | tr -d A,e command, A and e characters in LISTA file will be ignored.

```
root@kemal:~zeyno# cat LISTA
Ahmet
Mehmet
Ali
Veli
Zeyno
root@kemal:~zeyno# cat LISTA | tr -d A,e
hmt
Mhmt
li
Vli
Zyno
root@kemal:~zeyno# _
```

# Cmp

One of the commands that we can use to make comparisons between files is cmp command. For example, I use cmp hacker test command to compare two files called hacker and test. In result, it will display the difference in files, the line of first difference occured, and as byte number.