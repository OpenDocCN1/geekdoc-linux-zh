
⇒ Here are some ways to use this.

- To echo a backslash character, type:

```
$ echo '\' RET
\
$
```

- To echo the string "* ! \" /," type:

```
$ echo '* ! " /' RET
* ! " /
$
```

- To echo the string ""$HOSTNAME" is nice!", where there is a newline character after the second double quote character, type:

```
$ echo ""$HOSTNAME" RET
> is nice!' RET
"$HOSTNAME"
is nice!
$
```

NOTES: This second method is one of the simpler methods of quoting.

## METHOD #3

Quote a phrase by enclosing it in double quote characters (") to retain the special meaning of some characters: the dollar sign ($), backtick (`), exclamation point (!), and backslash (\).

This means that: Variables are expanded to their values (see Recipe 3.5 [Using Shell Variables], page 77), command output may be specified (see Recipe 3.1.11 [Specifying the Output of a Command as an Argument], page 65), command history may be referenced (see Recipe 3.4 [Using Your Command History], page 74), and single characters may be escaped, as described in Method #1 above.

You can pass single quote and newline characters; to pass double quotes, dollar signs, backticks, or backslashes, escape them first with a backslash (\). Pass an exclamation point by escaping it outside of the double quotes.

⇒ Here are some ways to use this.

- To echo “Isn’t it great?,” type:

```
$ echo "Isn't it great?" RET
Isn't it great?
$
```

- To echo “Isn’t $HOSTNAME it?,” type:

```
$ echo "Isn't \$HOSTNAME it?" RET
Isn't $HOSTNAME it?
$
```

- To echo “Isn’t this $HOSTNAME?,” where $HOSTNAME is a shell variable to be expanded, type:

```
$ echo "Isn't this $HOSTNAME?" RET
Isn't this lucky?
$
```

- To echo “Wow!
  This isn’t "$HOSTNAME"!,” where there is a newline character after the first exclamation point, type:

```
$ echo "Wow!"! RET
> This isn't "\$HOSTNAME"!" RET
Wow!
This isn't "$HOSTNAME"!
$
```

In the second-last example, the system’s hostname is lucky. In the second and the last examples, the text “$HOSTNAME” is quoted literally and is not expanded as a variable; by omitting the backslash directly preceding the dollar sign, the shell will expand the variable.

NOTES: You can sometimes get away with quoting an exclamation point in double quotes, but because it’s reserved for referencing your Bash command history, using it in the wrong context can have unexpected results. Unless you're only using the single quotes method, it's safest to escape an exclamation point outside of the double quotes.

## METHOD #4

To pass special characters as a string, give them as $'string', where string is the string of characters to be passed. This is called "ANSI-C style" quoting.

Special backslash escape sequences for certain characters are commonly included in a string, as listed in the following table.

| 转义序列 | 描述 |
|---|---|
| \a | Alert (rings the system bell). |
| \b | Backspace. |
| \e | Escape. |
| \f | Form feed. |
| \n | Newline. |
| \r | Carriage return. |
| \t | Horizontal tab. |
| \v | Vertical tab. |
| \\ | Backslash. |
| \NNN | Character whose ASCII code is NNN in octal (base 8). |

⇒ Here are some ways to use this.

- To echo the string “Hello” followed by two newline characters, type:

```
$ echo Hello$'\n\n' [RET]
Hello
$
```

- To echo a pilcrow sign character (octal character code 266), type:

```
$ echo $'\266' RET
¶
$
```

- To append a newline character and a pilcrow sign character (octal character code 266) to the file draft, type:

```
$ echo $'\n\266' >> draft RET
```

## 3.1.4 Letting the Shell Complete What You Type

*Completion* is when Bash does its best to finish your typing for you. To use it, press TAB on the input line, and the shell will *complete* the word to the left of the cursor to the best of its ability. Completion is one of those things that, once you begin to use it, you will wonder how you ever managed to get by without it.

Completion works on both file names and command names, depending on the context of the cursor when you press the TAB key.

When there is more than a single way to complete a word, the shell will beep¹ to alert you so; pressing TAB again will display the possible options, and then redraw your command line. If the options are many, the shell will ask you at that point whether you would really like them all displayed.

- To use completion to specify the /usr/lib/emacs/20.7/i386-debian-linux-gnu/ directory as an argument to the ls command, type:

```
$ ls /usr/lib/TAB rings the bell TAB
Display all 767 possibilities? (y or n)n
$ ls /usr/lib/e TAB rings the bell TAB
elm-me+ emacs emacs-common entity-map
$ ls /usr/lib/emac TAB rings the bell
$ ls /usr/lib/emacs TAB rings the bell
$ ls /usr/lib/emacs/ TAB
emacs emacs-common
$ ls /usr/lib/emacs/ TAB 20.7/ TAB i386-debian-linux-gnu/
```

> ¹ The UNIX way of saying this is that the command “rings the system bell.”
