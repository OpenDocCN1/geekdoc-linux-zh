# Negating an Expression

Negation reverses the result of a test expression. An expression that would have been true is treated as false and vice versa. The basic syntax of the negation operator is

```
test ! expr
```

or

```
[ ! expr ]
```

Here expr is any valid test expression.

The following example, taken from OpenBSD's /etc/rc startup script, illustrates the use of the ! operator:

```
if [ ! -f /etc/motd ]; then
    install -c -o root -g wheel -m 664 /dev/null /etc/motd
fi
```

This example creates the file /etc/motd (the message of the day on UNIX systems) using the install command if it does not exist or is not a regular file. The execution is as follows:

+   1. First the test
+      -f /etc/motd
+      is performed.
+   2. The result of the test is negated because of the ! operator. If the file /etc/motd exists and is a regular file, the compound expression returns false (!); otherwise, it returns true.
+   3. If the result of the previous step is true, the file /etc/motd is created; otherwise, the if statement performs no actions.

This example can also be written as either of the following commands:

```
test ! -f /etc/motd && install -c -o root -g wheel -m 664 /dev/null /etc/motd
[ ! -f /etc/motd ] && install -c -o root -g wheel -m 664 /dev/null /etc/motd
```

This achieves the same result because install is executed only if the test or [ commands return true.