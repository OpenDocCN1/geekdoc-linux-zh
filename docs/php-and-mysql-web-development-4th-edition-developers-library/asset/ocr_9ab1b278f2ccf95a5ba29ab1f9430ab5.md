```
+-----------------------+  
| NOW()                 |  
+-----------------------+  
| 2008-03-21 10:51:23   |  
+-----------------------+  
1 row in set (0.00 sec)
```

Another way to terminate a statement is to use \G (``go'') rather than a semicolon:

```
mysql> SELECT NOW()\G  
*************************** 1. row ***************************  
NOW(): 2008-03-21 10:51:28  
1 row in set (0.00 sec)
```

Or you can use \G, which displays the results in "vertical" format, one value per line:

```
mysql> SELECT NOW(), USER(), VERSION()\G  
*************************** 1. row ***************************  
NOW(): 2008-03-21 10:51:34  
USER(): sampadm@localhost  
VERSION(): 5.0.60-log  
1 row in set (0.03 sec)
```

For a statement that generates short output lines, \G is not so useful, but if the lines are so long that they wrap around on your screen, \G can make the output much easier to read.

*mysql* 1 displays the statement result and a line that shows the number of rows the result consists of and the time elapsed during statement processing. In subsequent examples, I usually will not show the row-count line.

Because *mysql* 1 waits for the statement terminator, you need not enter a statement all on a single line. You can spread it over several lines if you want:

```
mysql> SELECT NOW(),  
   -> USER(),  
   -> VERSION()  
   -> ;
```

```
+-----------------------+--------------------+----------------------+  
| NOW()                 | USER()             | VERSION()            |  
+-----------------------+--------------------+----------------------+  
| 2008-03-21 10:51:37   | sampadm@localhost  | 5.0.60-log           |  
+-----------------------+--------------------+----------------------+
```

Observe how the prompt changes from *mysql* > to -> after you enter the first line of the statement. That tells you that *mysql* 1 thinks you're still entering the statement, which is important feedback: If you forget the semicolon at the end of a statement, the changed prompt helps you realize that *mysql* is still waiting for something. Otherwise, you'll be