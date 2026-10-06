# Combining anchors

There are a couple of common situations where you can combine both the start and end anchor on the same line. In the first situation, suppose that you want to look for a line of data containing only a specific text pattern:

```
$ cat data4
is is a test of using both anchors
i said this is a test
this is a test
I'm sure this is a test.
$ sed -n '/^this is a test$/p' data4
this is a test
$
```

The sed editor ignores the lines that include other text besides the specified text.
The second situation may seem a little odd at first, but is extremely useful. By combining both anchors together in a pattern with no text, you can filter lines from the data stream. Look at this example:

```
$ cat data5
This is one test line.

This is another test line.
$ sed '/^$/d' data5
This is one test line.
This is another test line.
$
```

The regular expression pattern defined looks for lines that have nothing between the start and end of the line. Since blank lines contain no text between the two newline characters, they match the regular expression pattern. The sed editor uses the delete command to delete lines that match the regular expression pattern, removing all blank lines from the text. This is an effective way to remove blank lines from documents.

# The dot character

The special character is used to match any single character except a newline character. The dot character must match a character though; if there's no character in the place of the dot, then the pattern will fail.

Let's look at a few examples of using the dot character in a regular pattern:

```
$ cat data6
This is a test of a line.
The cat is sleeping.
That is a very nice hat.
This test is at line four.
```