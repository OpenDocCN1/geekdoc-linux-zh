```
factorial=$[ $factorial * $counter ]
=$[ $counter + 1 ]
done
```

```
result=`echo $factorial | sed '(
:start
s/.*([0-9])\)\([0-9])\(3\)/\1,\2/
t'
```

```
echo "The result is $result"
./fact 20
The result is 2,432,902,008,176,640,000
$
```

After you use the normal factorial calculation script, the result of that script is used as the input to the sed editor script, which adds commas. This value is then used in the echo statement to produce the result.

# Creating sed Utilities

As you've seen in the short examples presented so far in this chapter, there are lots of cool data-formatting things you can do with the sed editor. This section shows a few handy well-known sed editor scripts for performing common data-handling functions.

# Double spacing lines

To start things, take a look at a simple sed script to insert a blank line between lines in the text file:

```
$ sed 'G' data2
This is the header line.
```

This is the first data line.

This is the second data line.

This is the last line.

```
$
```

That was pretty simple! The key to this trick is the default value of the hold space. Remember, the 6 command simply appends the contents of the hold space to the current pattern space contents. When you start the sed editor, the hold space contains an empty line. By appending that to an existing line, you create a blank line after the existing line.