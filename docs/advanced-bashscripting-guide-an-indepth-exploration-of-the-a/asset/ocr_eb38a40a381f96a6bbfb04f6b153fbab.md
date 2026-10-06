```
echo "Test #2 succeeds."
else
echo "Test #2 fails."
fi
```

```
# -a and -o options provide
#+ an an alternative compound condition test.
# Thanks to Patrick Callahan for pointing this out.
```

```
if [ "$a" -eq 24 -a "$b" -eq 47 ]
then
echo "Test #3 succeeds."
else
echo "Test #3 fails."
fi
```

```
if [ "$a" -eq 98 -o "$b" -eq 47 ]
then
echo "Test #4 succeeds."
else
echo "Test #4 fails."
fi
```

```
a=rhino
b=crocodile
if [ "$a" = rhino ] && [ "$b" = crocodile ]
then
echo "Test #5 succeeds."
else
echo "Test #5 fails."
fi
```

```
exit 0
```

The && and || operators also find use in an arithmetic context.

```
bash$ echo $(( (1 6 2 )) $((3 6 0 )) $((4 || 0)) $((0 || 0))
1 0 1
```

# miscellaneous operators

comma operator

The comma operator chains together two or more arithmetic operations. All the operations are evaluated (with possible side effects), but only the last operation is returned.

```
let t1 = ((5 + 3, 7 - 1, 15 - 4))
echo t1 = \$t1      # t1 = 11
```

```
let t2 = ((9, 15 / 3))  # Set "a" and calculate "t2"
echo t2 = \$t2      a = \$5      a = 9
```

# 8. Operations and Related Topics