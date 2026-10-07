```
```
7      my_print (my_string);
8      my_print2 (my_string);
9   }
10
```
```

Press Enter and gdb executes the list command again, displaying the following output:

```
```
11   my_print (char *string)
12   {
13      printf ("The string is %s\n", string);
14   }
15
16   my_print2 (char *string)
17   {
18      char *string2;
19      int size, i;
20
```
```

Pressing Enter one more time lists the rest of the greeting program:

```
```
21   size = strlen (string);
22   string2 = (char *) malloc (size + 1);
23   for (i = 0; i < size; i++)
24      string2[size - i] = string[i];
25   string2[size+1] = '\0';
26   printf ("The string printed backward is %s\n", string2);
27   }
```
```

By listing the file, we can see that the place where we want to set the breakpoint is line 24. Now, to set the breakpoint, enter the following command at the gdb command prompt:

```
```
(gdb) break 24
```
```

gdb should now print a response resembling the following:

```
```
Breakpoint 1 at 0x139: file greeting.c, line 24
(gdb)
```
```

Now let’s run the program again by typing the run command. This command generates the following output:

```
```
Starting program: /root/greeting
The string is hello there
```
```

```
```
Breakpoint 1, my_print2 (string = 0xbffffdc4 "hello there") at greeting.c
==>24
24    string2[size-i]=string[i]
```
```

We can see what is actually going wrong with the program by setting a watch which tells the value of the string2[size - i] variable expression.