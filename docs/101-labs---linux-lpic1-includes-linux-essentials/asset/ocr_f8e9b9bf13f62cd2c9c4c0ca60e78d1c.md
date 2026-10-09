# **Task 3:**

To understand single quotes, double quotes, and backquotes, enter the following:

```
hello="echo ""hello"""
 echo ""$hello""
 echo '$hello'
 echo `$hello`
```

Double quotes allow for variables to have their values referenced. Single quotes are always literal, while backquotes *execute* the command (including variable references) within those quotes.

# **Task 4:**

Now run the following commands:

+   * `pwd`
+   * `which pwd`
+   * `uname -a`

Can you figure out what these commands do? If not, there's another command—*man*—which could help you get some information.

Run `set -v`, then run the above commands again. You’ve just set the verbose flag in Bash, which repeats every command as you run it. To unset it, just run `unset -v`...

Just kidding! The completely unintuitive way to *unset* the `-v` flag is to `set +v`—run `set --help` to get more information on what Bash has available for customization; there's quite a bit.

`unset` actually has a different purpose, which is to unset variables. Observe:

+   * `foo=123`
+   * `echo $foo`
+   * `unset foo`
+   * `echo $foo`

**Notes:**
In some cases, you will want to reference variables with the `${variable}` syntax. This is equivalent to `$variable`, but the reasons for choosing one over the other are beyond the scope of this lab.