```
default:
            die_now();
        }
        ++i;
    }
    return 0;
}

void die_now(void)
{
    printf("dying now\n");
    exit(1);
}
```

Be careful, when writing code that has an infinite loop like the `while` loop in this program, that an escape point exists, such as breaking out of the loop when a loop counter reaches a certain value. For our purposes, however, it perfectly illustrates how the case range extension works. The output of this program is

![](bbox=[0.03, 0.36, 0.14, 0.41])

# Output

```
$ ./nore
i = 0
i = 1
i = 2
i = 3
i = 4
i = 5
dying now
```

The case range extension behaves just as a regular case statement would. When `i` becomes 6, program flow reaches the `default` block, `die_now` executes, and the program terminates.

+   3. The final example illustrates the effect of using the packed attribute on a structure. The program merely prints the size of the structures and their constituent members.

![](bbox=[0.04, 0.68, 0.14, 0.72])

# Example

```
packme.c
/*
 * packme.c Using gcc's packed attributed
 */
```