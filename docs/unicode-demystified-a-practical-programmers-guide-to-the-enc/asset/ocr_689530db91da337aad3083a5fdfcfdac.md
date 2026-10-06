```
$ comm c d
aaaaaa
bbbbb
ccccc
ddddd
eeeee
fffff
ggggg
hhhhhh
```

The next example shows the use of options to prevent comm from displaying columns 1 and 2. The result column 3, a list of the lines common to files c and d.

```
$ comm -12 c d
ddddd
eeeee
```