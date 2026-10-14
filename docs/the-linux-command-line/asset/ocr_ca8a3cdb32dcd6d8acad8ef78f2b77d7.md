| Escape Sequence | Meaning |
|---|---|
| \a | Bell ("Alert" - causes the computer to beep) |
| \b | Backspace |
| \n | Newline. On Unix-like systems, this produces a linefeed. |
| \r | Carriage return |
| \t | Tab |

The table above lists some of the common backslash escape sequences. The idea behind this representation using the backslash originated in the C programming language and has been adopted by many others, including the shell.

Adding the "-e" option to echo will enable interpretation of escape sequences. You may also place them inside $' '. Here, using the sleep command, a simple program that just waits for the specified number of seconds and then exits, we can create a primitive countdown timer:

```
sleep 10; echo -e "Time's up\a"
```

We could also do this:

```
sleep 10; echo "Time's up" $'\a'
```

# Summing Up

As we move forward with using the shell, we will find that expansions and quoting will be used with increasing frequency, so it makes sense to get a good understanding of the way they works. In fact, it could be argued that they are the most important subjects to learn about the shell. Without a proper understanding of expansion, the shell will always be a source of mystery and confusion, and much of it potential power wasted.

# Further Reading

+   - The bash man page has major sections on both expansion and quoting which cover these topics in a more formal manner.
+   - The Bash Reference Manual also contains chapters on expansion and quoting: http://www.gnu.org/software/bash/manual/bashref.html