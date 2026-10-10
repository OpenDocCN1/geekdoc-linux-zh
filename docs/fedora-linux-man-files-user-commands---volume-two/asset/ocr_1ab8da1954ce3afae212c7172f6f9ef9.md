# HISTORICAL FEATURES

There is one feature of historical \(awk\) implementations that *gawk* supports: It is possible to call the `length()` built-in function not only with no argument, but even without parentheses! Thus,

```
    a = length     # Holy Algol 60, Batman!
```

is the same as either of

```
    a = length() a = length($0)
```

Using this feature is poor practice, and *gawk* issues a warning about its use if `—lint` is specified on the command line.