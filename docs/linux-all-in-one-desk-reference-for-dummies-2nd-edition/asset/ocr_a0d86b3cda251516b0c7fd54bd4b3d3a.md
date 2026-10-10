case value2:
    statement_2
break;
.
.
.
default:
    statement_default

If the *expression* being tested by switch evaluates to *value1*, *statement_1* executes. If the expression is equal to *value2*, *statement_2* executes. The value is compared with each case label and the statement following the matching label executes. If the value does not match any of the case labels, the block *statement_default* following the default label executes. Each statement ends with a break statement that separates the code of one case label from another. Here is a *switch* statement that calls different routines, depending on the value of an integer variable named *command*:

```
```
switch (command)
{
    case 'q':
        quit_app();
    case 'c':
        connect();
        break;
    case 's':
        set_params();
        break;
    case '?':
    case 'H':
        print_help();
        break;
    default:
        printf ("Unknown command!\n");
}
```
```

# ## The while statement

The *while* statement is used in the form
while (*expression*) *statement*

The *statement* executes until the *expression* evaluates to 0. A *while* statement evaluates the expression before each execution of the statement. Thus, a *while* loop executes the statement zero or more times. Here is a *while* statement for copying one array to another.