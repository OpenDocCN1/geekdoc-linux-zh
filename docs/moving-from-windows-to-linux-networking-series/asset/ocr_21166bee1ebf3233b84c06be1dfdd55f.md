![](bbox=[0.06, 0.03, 0.66, 0.23])

This may look a little complicated, and there are several rules to remember. Each choice must end with a double semicolon, the entire *case* statement must end with *esac*, and each choice is followed by a parenthesis. This may seem like a lot to remember, but with a little practice it will become very natural. This is also another technique that is common to most programming languages.

# Multiple Statements on One Line

Sometimes in your script you might have several related statements to write. You might want to put them all on one line. You could do this either to save space or to group commands that belong together logically. For whatever reason, doing it is simple. You separate each command on the line with a single semicolon, as you see here:

```
```python
statement one; statement two; statement three
```

```

Open your favorite text editor and enter the following. Then save it as *scriptmultiple.sh* and run it.

```
```
#!/bin/bash
ls; ps;who;logname;
exit 0
```

```

When you run this, it will work just as if you had placed each command on a separate line. You can see the results in Figure 21.10.

![](bbox=[0.06, 0.62, 0.66, 0.94])