If you define a space in the regular expression, it must appear in the data stream. You can even create a regular expression pattern that matches multiple contiguous spaces:

```
$ cat data1
This is a normal line of text.
This is a line with too many spaces.
$ sed -n '/p' data1
This is a line with too many spaces.
$ 
```

The line with two spaces between words matches the regular expression pattern. This is a great way to catch spacing problems in text files!

# ## Special characters

As you use text strings in your regular expression patterns, there's something you need to be aware of. There are a few **exceptions** when defining text characters in a regular expression. Regular expression patterns assign a special meaning to a few characters. If you try to use these characters in your text pattern, you won't get the results you were expecting.

These special characters are recognized by regular expressions:

```
. * [ ] ^ $ ( ) { } \\ ? | ( )
```

As the chapter progresses, you'll find out just what these special characters do in a regular expression. For now, however, just remember that you can't use these characters by themselves in your text pattern.

If you want to use one of the special characters as a text character, you need to *escape* it. When you escape the special characters, you add a special character in front of it to indicate to the regular expression engine that it should interpret the next character as a normal text character. The special character that does this is the backslash character (\\).

For example, if you want to search for a dollar sign in your text, just precede it with a backslash character:

```
$ cat data2
The cost is $4.00
$ sed -n '/\$/' data2
The cost is $4.00
$ 
```

Because the backslash is a special character, if you need to use it in a regular expression pattern, you need to escape it as well, producing a double backslash:

```
$ echo "\\ is a special character" | sed -n '/\\\\/p'
\\ is a special character
$ 
```