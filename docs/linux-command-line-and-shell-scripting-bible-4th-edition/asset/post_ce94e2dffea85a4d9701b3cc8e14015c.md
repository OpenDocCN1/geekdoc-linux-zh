
## Replacing individual words

The ampersand symbol retrieves the entire string that matches the pattern you specify in the substitution command. Sometimes, you'll want to retrieve only a subset of the string. You can do that, too, but it's a little tricky.

The sed editor uses parentheses to define a substring component within the substitution pattern. You can then reference each substring component using a special character in the replacement pattern. The replacement character consists of a backslash and a number. The number indicates the substring component's position. The sed editor assigns the first component the character \1, the second component the character \2, and so on.

### NOTE

> When you use parentheses in the substitution command, you must use the escape character to identify them as grouping characters and not normal parentheses. This is the reverse of when you escape other special characters.

Look at an example of using this feature in a sed editor script:

```bash
$ echo "The Guide to Programming" | \
> sed 's/\(^Guide to\) Programming/^\1 DevOps/'
    The Guide to DevOps
$
```

This substitution command uses one set of parentheses around *Guide to*, identifying it as a substring component. It then uses the \1 in the replacement pattern to recall the first identified component. This isn't too exciting, but it can really be useful when working with wildcard patterns.

Suppose you need to replace a phrase with just a single word that's a substring of the phrase, but that substring just happens to be using a wildcard character. In such cases, using substring components is a lifesaver:

```bash
$ echo "That furry cat is pretty." | \
> sed 's/furry \(.at\)/\1/'
That cat is pretty.
$
$ echo "That furry hat is pretty." | \
> sed 's/furry \(.at\)/\1/'
That hat is pretty.
$
```

In this situation, you can't use the ampersand symbol, because it would replace the entire matching pattern. The substring component provides the answer, allowing you to select just which part of the pattern to use as the replacement pattern.

This feature can be especially helpful when you need to insert text between two or more substring components. Here's a script that uses substring components to insert a comma in long numbers:

```bash
$ echo "1234567" | sed '{ \
> :start \
> s/^(.*[0-9])\([0-9]\{3\}\)/\1,\2/2 \
> t start }'
1,234,567
$
```

The script divides the matching pattern into two components:

- `.*[0-9]`
- `[0-9]{3}`

This pattern looks for two substrings. The first substring is any number of characters ending in a digit. The second substring is a series of three digits (see Chapter 20, “Regular Expressions,” for information about how to use braces in a regular expression). If this pattern is found in the text, the replacement text puts a comma between the two components, each identified by its component position. The script uses the test (t) command to iterate through the number until all commas have been put in their proper place.

## Placing sed Commands in Scripts

Now that you've seen the various parts of the `sed` editor, it's time to put them together and use them in your shell scripts. This section demonstrates some of the features that you should know about when using the `sed` editor in your Bash shell scripts.

### Using wrappers

You may have noticed that trying to implement a `sed` editor script can be cumbersome, especially if the script is long. Instead of having to retype the entire script each time you want to use it, you can place the `sed` editor command in a shell script *wrapper*. The wrapper acts as a go-between for the `sed` editor script and the command line. A shell script wrapper, `ChangeScriptShell.sh`, was used back in **Chapter 19** as a practical example.

Once inside the shell script, you can use normal shell variables and parameters with your `sed` editor scripts. Here's an example of using the command-line parameter variable as the input to a `sed` script:

```bash
$ cat reverse.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to reverse test file lines.
#
sed -n '{1!G; h; $p}' $1
#
exit
$
```

The shell script called `reverse.sh` uses the `sed` editor script to reverse text lines in a data stream. It uses the `$1` shell parameter to retrieve the first parameter from the command line, which should be the name of the file to reverse:

```bash
$ cat data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
$ ./reverse.sh data2.txt
End of Data Lines
Second Data Line
First Data Line
Header Line
$
```

Now you can easily use the sed editor script on any file without having to constantly retype the entire sed command line.

### Redirecting sed output

By default, the sed editor outputs the results of the script to STDOUT. You can employ all the standard methods of redirecting the output of the sed editor in your shell scripts.

You can use dollar sign/parenthesis, `$()`, to redirect the output of your sed editor command to a variable for use later in the script. The following is an example of using the sed script to add commas to the result of a numeric computation:

```bash
$ cat fact.sh
#!/bin/bash
# Shell wrapper for sed editor script
# to calculate a factorial, and
# format the result with commas.
#
factorial=1
counter=1
number=$1
#
while [ $counter -le $number ]; do
    factorial=$[ $factorial * $counter ]
    counter=$[ $counter + 1 ]
done
#
result=$(echo $factorial | sed '{
:start
s/^\(.\*[0-9]\)\([0-9]\{3\}\)/\1,\2/
t start
}')
# echo "The result is $result"
#
exit
$ ./fact.sh 20
$ The result is 2,432,902,008,176,640,000
```

After you use the normal factorial calculation script, the result of that script is used as the input to the sed editor script, which adds commas. This value is then used in the `echo` statement to produce the result. And how nice to now have that long sed script within a Bash shell script so that you can use it without typing all the sed commands in again!

## Creating sed Utilities

As you’ve seen in the short examples presented so far in this chapter, you can do lots of cool data-formatting things with the sed editor. This section shows a few handy well-known sed editor scripts for performing common data-handling functions.

### Spacing with double lines

To start things off, look at a simple sed script to insert a blank line between lines in a text file:

```bash
$ sed 'G' data2.txt
Header Line

First Data Line

Second Data Line

End of Data Lines

$
```

That was pretty simple! The key to this trick is the default value of the hold space. Recall that the `g` command simply appends the contents of the hold space to the current pattern space contents. When you start the sed editor, the hold space contains an empty line. By appending that to an existing line, you create a blank line after the existing line.

You may have noticed that this script also adds a blank line to the last line in the data stream, producing a blank line at the end of the file. If you want to get rid of this, you can use the negate symbol and the last line symbol to ensure that the script doesn't add the blank line to the last line of the data stream:

```bash
$ sed '$!G' data2.txt
Header Line
First Data Line
Second Data Line
End of Data Lines
$
```

Now that looks a little better. As long as the line isn't the last line, the `g` command appends the contents of the hold space. When the sed editor gets to the last line, it skips the `g` command.

### Spacing files that may have blanks

To take double spacing one step further, what if the text file already has a few blank lines but you want to double-space all the lines? If you use the previous script, you'll get some areas that have too many blank lines, because each existing blank line gets doubled:

```bash
$ cat data6.txt
Line one.
Line two.
Line three.
Line four.
$
$ sed '$!G' data6.txt
Line one.
Line two.
Line three.
Line four.
$
```

Now we have three blank lines where the original blank line was located. The solution to this problem is to first delete any blank lines
