⇒ Here are some ways to use this.

+   - To echo “Isn’t it great?,” type:

```
$ echo "Isn't it great?" RET
Isn't it great?
$
```

+   - To echo “Isn’t $HOSTNAME it?,” type:

```
$ echo "Isn't \$HOSTNAME it?" RET
Isn't $HOSTNAME it?
$
```

+   - To echo “Isn’t this $HOSTNAME?,” where $HOSTNAME is a shell variable to be expanded, type:

```
$ echo "Isn't this $HOSTNAME?" RET
Isn't this lucky?
$
```

+   - To echo “Wow!
+   This isn’t "$HOSTNAME"!,” where there is a newline character after the first exclamation point, type:

```
$ echo "Wow!"! RET
> This isn't "\$HOSTNAME"!" RET
Wow!
This isn't "$HOSTNAME"!
$
```

In the second-last example, the system’s hostname is lucky. In the second and the last examples, the text “$HOSTNAME” is quoted literally and is not expanded as a variable; by omitting the backslash directly preceding the dollar sign, the shell will expand the variable.

NOTES: You can sometimes get away with quoting an exclamation point in double quotes, but because it’s reserved for referencing your Bash command history, using it in the wrong context can have unexpected results. Unless