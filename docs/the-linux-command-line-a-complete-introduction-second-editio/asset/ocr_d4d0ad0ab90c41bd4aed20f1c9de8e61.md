```
title="System Information Report"
echo "<html>"
    <head>
        <title>$title</title>
    </head>
    <body>
        <h1>$title</h1>
    </body>
</html>"
```

By creating a variable named title and assigning it the value System Information Report, we can take advantage of parameter expansion and place the string in multiple locations.

So, how do we create a variable? Simple, we just use it. When the shell encounters a variable, it automatically creates it. This differs from many programming languages in which variables must be explicitly declared or defined before use. The shell is very lax about this, which can lead to some problems. For example, consider this scenario played out on the command line:

```
[me@linuxbox ~]$ foo="yes"
[me@linuxbox ~]$ echo $foo
yes
[me@linuxbox ~]$ echo $foo1
[me@linuxbox ~]$
```

We first assign the value yes to the variable foo, and then we display its value with echo. Next we display the value of the variable name misspelled as foo1 and get a blank result. This is because the shell happily created the variable foo1 when it encountered it and gave it the default value of nothing, or empty. From this, we learn that we must pay close attention to our spelling! It's also important to understand what really happened in this example. From our previous look at how the shell performs expansions, we know that the following command:

```
[me@linuxbox ~]$ echo $foo
```

undergoes parameter expansion and results in the following: