> **NOTE**
Notice that in the `tcsh` example the first line starts with a `#`. This is required for `tcsh` to recognize the file containing the commands as a `tcsh` script file.

# The case Statement

The case statement enables you to compare a pattern with several other patterns and execute a block of code if a match is found. The shell case statement is quite a bit more powerful than the case statement in Pascal or the switch statement in C. This is because in the shell case statement you can compare strings with wildcard characters in them, whereas with the Pascal and C equivalents, you can only compare enumerated types or integer values.

Once again, the syntax for the case statement is identical for bash and `pdksh` and different for `tcsh`. The syntax for bash and `pdksh` is the following:

```
case string1 in
    str1)
        commands;;
    str2)
        commands;;
    *)
        commands;;
esac
```

`string1` is compared to `str1` and `str2`. If one of these strings matches `string1`, all commands up to the double semicolon (`;;`) are executed. If neither `str1` nor `str2` matches `string1`, the commands associated with the asterisk are executed. This is the default case condition because the asterisk matches all strings.

The `tcsh` equivalent of the bash and `pdksh` case statement is called the switch statement. This statement’s syntax closely follows the C switch statement syntax. Here it is:

```
switch (string1)
    case str1:
        statements
    breaks
    case str2:
        statements
    breaks
    default:
        statements
    breaks
end
```