```
address:
    address {
        command1
        command2
        command3
    }
```

The sed editor applies each of the commands you specify only to lines that match the address specified. This section demonstrates using both of these addressing techniques in your sed editor scripts.

# ## Addressing the numeric line

When using numeric line addressing, you reference lines using their line position in the text stream. The sed editor assigns the first line in the text stream as line number 1 and continues sequentially for each new line.

The address you specify in the command can be a single line number or a range of lines specified by a starting line number, a comma, and an ending line number. Here's an example of specifying a line number to which the sed command will be applied:

```
$ cat data1.txt
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy dog.
    $
    $ sed '2s/dog/cat/' data1.txt
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy cat.
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy dog.
    $
```

The sed editor modified the text only in line 2 per the address specified. Here's another example, this time using a range of line addresses (lines 2 through 3):

```
$ sed '2,3s/dog/cat/' data1.txt
    The quick brown fox jumps over the lazy dog.
    The quick brown fox jumps over the lazy cat.
    The quick brown fox jumps over the lazy cat.
```