Remainder  The remainder operator (`%`) gives the remainder when its first operand is divided by its second. For example, the expression `$((15%7))` has the value 1.

Boolean  The result of a Boolean operation is either 0 (*false*) or 1 (*true*).

The `&&` (AND) and `||` (OR) Boolean operators are called *short-circuiting* operators. If the result of using one of these operators can be decided by looking only at the left operand, the right operand is not evaluated. The `&&` operator causes the shell to test the exit status of the command preceding it. If the command succeeded, `bash` executes the next command; otherwise, it skips the remaining commands on the command line. You can use this construct to execute commands conditionally:

```
$ mkdir bkup && cp -r src bkup
```

This compound command creates the directory **bkup**. If `mkdir` succeeds, the contents of directory **src** is copied recursively to **bkup**.

The `||` separator also causes `bash` to test the exit status of the first command but has the opposite effect: The remaining command(s) are executed only if the first one failed (that is, exited with nonzero status):

```
$ mkdir bkup || echo "mkdir of bkup failed" >> /tmp/log
```

The exit status of a command list is the exit status of the last command in the list. You can group lists with parentheses. For example, you could combine the previous two examples as

```
$ (mkdir bkup && cp -r src bkup) || echo "mkdir failed" >> /tmp/log
```

In the absence of parentheses, `&&` and `||` have equal precedence and are grouped from left to right. The following examples use the `true` and `false` utilities. These utilities do nothing and return `true` (0) and `false` (1) exit statuses, respectively:

```
$ false; echo $?
1
```

The `$?` variable holds the exit status of the preceding command (page 930). The next two commands yield an exit status of 1 (*false*):

```
$ true || false && false
$ echo $?
1
$ (true || false) && false
$ echo $?
1
```

Similarly the next two commands yield an exit status of 0 (*true*):

```
$ false && false || true
$ echo $?
0
$ (false && false) || true
$ echo $?
0
```