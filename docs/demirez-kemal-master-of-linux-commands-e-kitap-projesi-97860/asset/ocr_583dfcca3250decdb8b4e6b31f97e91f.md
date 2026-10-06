```
root@kemal:~/zeyno# cat LISTA
Ahmet
Mehmet
Ali
Veli
Zeyno
root@kemal:~/zeyno# cat LISTB
12345
54345
98768
76567
89087
root@kemal:~/zeyno# paste LIST LISTB
Ahmet 12345
Mehmet 54345
Ali 98768
Veli 76567
Zeyno 89087
root@kemal:~/zeyno# _
```

If you want, you can combine the contents of these files and you can redirect to a new file. For example, when we use paste LIST LISTB > LISTC command, the next contents of two files side by side in mutual line and at the same time creating a new file named LISTC will be saved into the file.

```
root@kemal:~/zeyno# paste LISTA LISTB > LISTC
root@kemal:~/zeyno# cat LISTC
Ahmet 12345
Mehmet 54345
Ali 98768
Veli 76567
Zeyno 89087
root@kemal:~/zeyno# _
```