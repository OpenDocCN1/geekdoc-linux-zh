```
`*argcp = i;
return true;

EC_CLEANUP_BGN
    EC_FLUSH("getargs*")
    return false;
EC_CLEANUP_END
}`
```

Comments:

+   - `getargs` returns `true` if it parsed the arguments OK, and otherwise `false`.
+   - It uses the standard C function `fgets` to read a line of input. The function is safe enough if a long line is typed, since it won’t overrun the buffer we pass in. But in that case we don’t want to leave the unread characters to be read later, as they would then be an unintended, and potentially damaging, shell command in their own right. So in that case (no newline terminator) we read in and throw away the rest of the line before printing an error message.
+   - Then we use `strtok` to break up the line into its arguments. (We also used `strtok` in `execvp2`, in the previous section.)
+   - `getargs` displays its own error messages with `EC_FLUSH` in case of a genu- ine error from one of the library functions it calls, and otherwise—such as in the case of a line that’s too long—prints a message for the user.

Next, we need functions to handle the built-in commands, `assignment` and `set`. These are easy, since we can use the environment-manipulation techniques from Section 5.2:

```
`extern char **environ;

void set(int argc, char *argv[])
{
    int i;

    if (argc != 1)
        printf("Extra args\n");
    else
        for (i = 0; environ[i] != NULL; i++)
            printf("%s\n", environ[i]);
}

void ass(int argc, char *argv[])
{
    char *name, *val;`
```