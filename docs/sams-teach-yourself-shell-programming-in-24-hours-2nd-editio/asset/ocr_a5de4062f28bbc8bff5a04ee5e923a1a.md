Here str1 and str2 are the two strings being compared. If these two strings are equal, the test succeeds and returns true (0). If the two strings are not equal, the test fails and returns false (1).

The following example, slightly modified from OpenBSD's /etc/rc, illustrates a common use of string comparisons:

```
# if $portmap == YES, the portmapper is started.
if [ "$portmap" = "YES" ]; then
    echo -n 'portmap'; portmap
fi
```

Here str1 is the value of $portmap and str2 is the string YES. The if statement uses the = operator to determine whether the value stored in $portmap is equal to YES. If $portmap is equal to YES, a message is issued and the program portmap is executed.

Note that $portmap is quoted in this example. Just like in previous examples, quoting is used to prevent problems resulting from variable substitution when $portmap happens to be unset or null. If $portmap was not quoted and it happened to be null, an error message similar to the following would be produced:

test: argument expected

An alternative technique for quoting is sometimes used to avoid these types of errors. Basically it involves prefixing str1 and str2 with an extra character, usually X. The syntax for this technique is

```
test X$str1 = X$str2
or
[ X$str1 = X$str2 ]
```

If either str1 or str2 is null, the string X is used instead of null. Rewriting the previous example using this technique yields:

```
# if $portmap == YES, the portmapper is started.
if [ X$portmap = X'YES' ]; then
    echo -n 'portmap'; portmap
fi
```

If $portmap is null then the strings X and XYES are compared; because these strings do not match, the test fails. If $portmap is YES then the strings XYES and XYES are compared; because these strings match, the test succeeds.