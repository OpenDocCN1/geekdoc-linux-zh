# 200 | Master of Linux Commands

```
root@kemal:~# cat list
AK12Ara, Istan45Bul, 2344, NewYork33
root@kemal:~# sed "s/[^1-9a-z]//g"
n12ratan45u2344work33
root@kemal:~# _
```

If there is a phrase in the file includes special characters which sed can detect them as operators, to make changes relating to these statements we can use backslash (\). This symbol prevents the next character after itself perceived as a regular string(expression). For example, lets say we have a file named example and there is an expression /etc/passwd in it. We can use backslash to replace this expression with expression named important we also can use other practical methods. We can do this with the following three commands:

+   - sed "s/etc/passwd/important/g" example
- sed "s_/etc/passwd_important_g" example
- sed ":/etc/passwd:important:g" example

```
root@kemal:~# cat example
/etc/passwd file
root@kemal:~# sed "s\/etc/passwd/important/g" example
important file
root@kemal:~# sed "s_/etc/passwd_important_g" example
important file
root@kemal:~# sed "s\/etc/passwd:important:g" example
important file
root@kemal:~# _
```

The characters we want sed change with another character in a text file, we need to use sed "y/./../" <file> mold. For example, in our tests file to change i to I, e to E, g to G we can use sed "y/ieg/IEG/" test command.

§