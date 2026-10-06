You also don't have to limit yourself to single text words in the regular expression. You can include spaces and numbers in your text string as well:

```
$ echo "This is line number 1" | sed -n '/ber 1/p'
This is line number 1
$
```

Spaces are treated just like any other character in the regular expression:

```
$ echo "This is line number1" | sed -n '/ber 1/p'
$
```

If you define a space in the regular expression, it must appear in the data stream. You can even create a regular expression pattern that matches contiguous spaces:

```
$ cat datal
This is a normal line of text.
This is a line with too many spaces.
$ sed -n ' / /p datal
This is a line with too many spaces.
$
```

The line with two spaces matches the regular expression pattern. This is a great way to catch spacing problems in text files!

# Special characters

As you use text strings in your regular expression patterns, there's something you need to be aware of. There are a few exceptions when defining text characters in a regular expression. Regular expression patterns assign a special meaning to a few characters. If you try to use these characters in your text pattern, you won't get the results you were expecting.

The special characters recognized by regular expressions are:

*.[^$|\?()

As the chapter progresses, you'll find out what these special characters do in a regular expression. For now though, just remember that you can't use these characters by themselves in your text pattern.

If you want to use one of the special characters as a text character, you need to escape it. When you escape the special characters, you add a special character in front of it to indicate to the regular expression engine that should interpret the next character as a normal text character. The special character that does this is the backslash character (\).