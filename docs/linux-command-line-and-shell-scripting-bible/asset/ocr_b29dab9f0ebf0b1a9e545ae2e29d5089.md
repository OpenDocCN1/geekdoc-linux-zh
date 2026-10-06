# The Linux Command Line

Fancy! If you need to compress multiple blank lines into a single blank line, use the -s parameter:
$ cat -s testl

This is a test file.

That we'll use to test the cat command.

If, you don't want tabs to appear, use the -T parameter:

```
$ cat -T testl
hello
```

This is a test file.

That we'll use^Itest the cat command.
$

The -T replaces any tabs in the text with the ^I character combination.

FIGURE 3-4

Using the more command to display a test file

![](bbox=[0.178, 0.535, 0.853, 0.873])

86