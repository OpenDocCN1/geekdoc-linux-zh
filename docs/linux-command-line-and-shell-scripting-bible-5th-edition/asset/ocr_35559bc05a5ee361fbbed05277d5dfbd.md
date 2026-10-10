```
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick green toad jumps over the lazy dog.
The quick green toad jumps over the sleeping dog.
$ 
```

The sed editor applies all the commands to all the lines in the address range.

# Deleting lines

The text substitution command isn't the only command available in the sed editor. If you need to delete specific lines of text in a text stream, you can use the delete command.

The delete (d) command pretty much does what it says. It deletes any text lines that match the addressing scheme supplied. Be careful with the d command, because if you forget to include an addressing scheme, all the lines are deleted from the stream:

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
$ sed 'd' data1.txt
$ 
```

The d command is obviously most helpful when used in conjunction with a specified address. This allows you to remove specific lines of text from the data stream, either by line number:

```
$ cat data6.txt
This is line number 1.
This is line number 2.
This is the 3rd line.
This is the 4th line.
$
$ sed '3d' data6.txt
This is line number 1.
This is line number 2.
This is the 4th line.
$ 
```

or by a specific range of lines:

```
$ sed '2,3d' data6.txt
This is line number 1.
This is the 4th line.
$ 
```

or by using the special end-of-file character:

```
$ sed '3,$d' data6.txt
This is line number 1.
This is line number 2.
$ 
```