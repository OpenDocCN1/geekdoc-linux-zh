More on Loops 179

```
> echo i
> done | wc -l
4$
```

# Typing a Loop on One Line

If you find yourself typing in loops directly at the command line, you might want to try using shorthand notation to type in an entire command on a single line: Put a semicolon after the last item in the list and one after each command in the loop (but not after the do).

Using this shorthand, the loop

```
for i in 1 2 3 4
do
  echo i
```

can be written

```
for i in 1 2 3 4; do echo i; done
```

You can type it directly on the command line this way:

```
$ for i in 1 2 3 4; do echo i;
1
2
3
4
$
```

The same rules apply to while and until loops.

if commands can also be typed on the same line using a similar format:

```
$ if [ 1 = 1 ]; then echo yes; fi
yes
$ if [ 1 = 2 ]; then echo yes; else echo no; fi
no$
```

Note that no semicolons appear after the then and the else.

Many shell programmers use a hybrid structure where if statements are structured thus:

```
if [ condition ]; then
  command
fi
```

This simple usage of the semicolon can help increase the readability of your shell programs and is worth considering as part of your own code formatting.