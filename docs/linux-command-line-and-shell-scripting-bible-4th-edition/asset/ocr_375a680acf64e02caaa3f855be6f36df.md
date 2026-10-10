The transform command performs a one to one mapping of the *inchars* and the *outchars* values. The first character in *inchars* is converted to the first character in *outchars*. The second character in *inchars* is converted to the second character in *outchars*. This mapping continues throughout the length of the specified characters. If the *inchars* and *outchars* are not the same length, the sed editor produces an error message.

Here's a simple example of using the transform (y) command:

```
```
$ cat data9.txt
This is line 1.
This is line 2.
This is line 3.
This is line 4.
This is line 5.
This is line 1 again.
This is line 3 again.
This is the last file line.
$ sed 'y/123/789/' data9.txt
This is line 7.
This is line 8.
This is line 9.
This is line 4.
This is line 5.
This is line 7 again.
This is line 9 again.
This is the last file line.
$ 
```
```

As you can see from the output, each instance of the characters specified in the *inchars* pattern has been replaced by the character in the same position in the *outchars* pattern.

The transform (y) command is a global command; that is, it performs the transformation on any character found in the text line automatically, without regard to the occurrence:

```
```
$ echo "Test #1 of try #1." | sed 'y/123/678/'
Test #6 of try #6.
$ 
```
```

The sed editor transformed both instances of the matching character 1 in the text line. You can't limit the transformation to a specific