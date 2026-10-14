
February 2012
Su Mo Tu We Th Fr Sa
1 2 3 4
5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29

In the first instance, the unquoted command substitution resulted in a command line with containing 38 arguments; in the second, the result was a command line with 1 argument that includes the embedded spaces and newlines.

## Single Quotes

If we need to suppress all expansions, we use single quotes. Here is a comparison of unquoted, double quotes, and single quotes:

```
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/is-output.txt a b foo 4 me
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text /*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo text '/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text /*.txt {a,b} $(echo foo) $((2+2)) $USER
```

As we can see, with each succeeding level of quoting, more and more expansions are suppressed.

## Escaping Characters

Sometimes we want to quote only a single character. To do this, we can precede a character with a backslash, which in this context is called the escape character. Often this is done inside double quotes to selectively prevent an expansion.

```
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning to the shell. These would include $, !, &, (a space), and others. To include a special character in a filename, you can do this:

```
[me@linuxbox ~]$ mv bad\&filename good_filename
```

To allow a backslash character to appear, escape it by typing \\. Note that within single quotes, the backslash loses its special meaning and is treated as an ordinary character.

## BACKSLASH ESCAPE SEQUENCES

In addition to its role as the escape character, the backslash is also used as part of a notation to represent certain special characters called control codes. The first 32 characters in the ASCII coding scheme are used to transmit commands to teletype-like devices. Some of these codes are familiar (tab, backspace, line-feed, and carriage return), while others are not (null, end-of-transmission, and acknowledge), as shown in Table 7-2.

## Table 7-2: Backslash Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| \a | Bell ("alert"—causes the computer to beep) |
| \b | Backspace |
| \n | Newline (on Unix-like systems, this produces a linefeed) |
| \r | Carriage return |
| \t | Tab |

This table lists some of the common backslash escape sequences. The idea behind using the backslash originated in the C programming language and has been adopted by many others, including the shell.

Adding the -e option to echo will enable interpretation of escape sequences. You may also place them inside $' '. Here, using the sleep command, a simple program that just waits for the specified number of seconds and then exits, we can create a primitive countdown timer.

```
sleep 10; echo -e "Time's up\a"
```

We could also do this:

```
sleep 10; echo "Time's up" $'\a'
```

## Final Note

As we move forward with using the shell, we will find that expansions and quoting will be used with increasing frequency, so it makes sense to get a good understanding of the way they work. In fact, it could be argued that they are the most important subjects to learn about the shell. Without a proper understanding of expansion, the shell will always be a source of mystery and confusion, and much of its potential power will be wasted.

## 8

## ADVANCED KEYBOARD TRICKS

I often kiddingly describe Unix as “the operating system for people who like to type.” Of course, the fact that it even has a command line is a testament to that. But command line users don’t like to type that much. Why else would so many commands have such short names, like cp, ls, mv, and rm?

In fact, one of the most cherished goals of the command line is laziness—doing the most work with the fewest keystrokes. Another goal is never having to lift your fingers from the keyboard—never reaching for the mouse. In this chapter, we will look at bash features that make keyboard use faster and more efficient.

The following commands will make an appearance:

- clear—Clear the screen.
- history—Display the contents of the history list.
