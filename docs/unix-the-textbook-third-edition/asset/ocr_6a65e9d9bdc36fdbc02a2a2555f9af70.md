```
elif expression2
    elif1-commands
elif expression3
    elif2-commands
...
else
    else-commands
fi

Purpose: To implement multiway branching
```

If expression1 is true, the commands in then-commands are executed. If expression1 is false, expression2 is evaluated, and if it is true, the commands in elif1-commands are executed. If expression2 is also false, expression3 is evaluated. If expression3 is true, the commands in elif2-commands are executed. If expression3 is also false, the commands in else-commands are executed. The execution of any command list is followed by the execution of the command after fi. You can use any number of elifs in an if statement to implement multiway branching. The semantics of the statement are depicted in Figure 12.3.

We modify the script in the if_demo file so that, if the command line argument is a directory, the program displays the number of files and subdirectories in the directory, excluding the hidden files. In addition, the program ensures that the command line argument is an existing file or directory in the current directory before processing it. In addition to using two if statement, we also use the if-then-elif-else-fi statement in

![](bbox=[0.15, 0.82, 0.88, 0.95])