
```
END {
    print "This concludes the listing"
}
$
```

This script uses the BEGIN script to create a header section for the report. It also defines a special variable called `FS`. This is yet another way to define the field separation character. This way, you don't have to depend on the script's user to define the field separation character in the command line options.

Here's a somewhat truncated output from running this `gawk` program script:

```
$ gawk -f script4.gawk /etc/passwd
The latest list of users and shells
UserID          Shell
--------    --------
root        /bin/bash
daemon      /usr/sbin/nologin
[...]
christine   /bin/bash
sshd        /usr/sbin/nologin
This concludes the listing
$
```

As expected, the BEGIN script created the header text, the program script processed the information from the specified data file (the `/etc/passwd` file), and the END script produced the footer text. The `\t` within the `print` command produces some nicely formatted tabbed output.

This gives you a small taste of the power available through using simple `gawk` scripts. Chapter 22, "Advanced `gawk`", describes some more basic programming principles available for your `gawk` scripts, along with some even more advanced programming concepts you can use in your `gawk` program scripts to create professional-looking reports from even the most cryptic data files.

## Looking at the `sed` Editor Basic Commands

The key to successfully using the `sed` editor is to know its myriad of commands and formats, which help you to customize your text editing.

This section describes some of the basic commands and features you can incorporate into your script to start using the sed editor.

### Introducing more substitution options

We've already covered how to use the s command to substitute new text for the text in a line. However, a few additional options are available for the s command that can help make your life easier.

### Substituting flags

There's a caveat to how the s command replaces matching patterns in the text string. Watch what happens in this example:

```
$ cat data4.txt
This is a test of the test script.
This is the second test of the test script.
$
$ sed 's/test/trial/' data4.txt
This is a trial of the test script.
This is the second trial of the test script.
$
```

The s command works fine in replacing text in multiple lines, but by default, it replaces only the first occurrence in each line. To get the s command to work on different occurrences of the text, you must use a substitution flag. The substitution flag is set after the substitution command strings:

```
s/pattern/replacement/flags
```

Four types of substitution flags are available:

- A number, indicating the pattern occurrence for which new text should be substituted
- g, indicating that new text should be substituted for all occurrences of the existing text
- p, indicating that the contents of the original line should be printed
- w file, which means to write the results of the substitution to a file

In the first type of substitution, you can specify which occurrence of the matching pattern the sed editor should substitute new text for:

```
$ sed 's:/test/trial/2/' data4.txt
This is a test of the trial script.
This is the second test of the trial script.
$
```

As a result of specifying a 2 as the substitution flag, the sed editor replaces the pattern only in the second occurrence in each line. The g substitution flag enables you to replace every occurrence (global) of the pattern in the text:

```
$ sed 's:/test/trial/g/' data4.txt
This is a trial of the trial script.
This is the second trial of the trial script.
$
```

The p substitution flag prints a line that contains a matching pattern in the substitute command. This is most often used in conjunction with the -n sed option:

```
$ cat data5.txt
This is a test line.
This is a different line.
$
$ sed -n 's:/test/trial/p/' data5.txt
This is a trial line.
$
```

The -n option suppresses output from the sed editor. However, the p substitution flag outputs any line that has been modified. Using the two in combination produces output only for lines that have been modified by the substitute command.

The w substitution flag produces the same output but stores the output in the specified file:

```
$ sed 's:/test/trial/w test.txt/' data5.txt
This is a trial line.
This is a different line.
$
$ cat test.txt
This is a trial line.
$
```

The normal output of the `sed` editor appears in `STDOUT`, but only the lines that include the matching pattern are stored in the specified output file.

### Replacing characters

Sometimes, you run across characters in text strings that aren't easy to use in the substitution pattern. One popular example in the Linux world is the forward slash (/).

Substituting pathnames in a file can get awkward. For example, if you wanted to substitute the C shell for the Bash shell in the `/etc/passwd` file, you'd have to do this:

```
$ sed 's/\bin\bash/\bin\csh/' /etc/passwd
```

Because the forward slash is used as the string delimiter, you must use a backslash to escape it if it appears in the pattern text. This often leads to confusion and mistakes.

To solve this problem, the `sed` editor allows you to select a different character for the string delimiter in the substitute command:

```
$ sed 's!/bin/bash!/bin/csh!' /etc/passwd
```

In this example, the exclamation point (!) is used for the string delimiter, making the pathnames much easier to read and understand.

### Using addresses

By default, the commands you use in the `sed` editor apply to all lines of the text data. If you want to apply a command only to a specific line or a group of lines, you must use *line addressing*.

There are two forms of line addressing in the `sed` editor:

- A numeric range of lines
- A text pattern that matches text within a line

Both forms use the same format for specifying the address:

```
[*address*] *command*
```

You can also group more than one command together for a specific address:

```
address {
    command1
    command2
    command3
}
```

The sed editor applies each of the commands you specify only to lines that match the address specified. This section demonstrates using both of these addressing techniques in your sed editor scripts.

### Addressing the numeric line

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
    The quick brown fox jumps over the lazy dog.
    $
```

If you want to apply a command to a group of lines starting at some point within the text but continuing to the end of the text, you can use a dollar sign in place of the last address range number:

```
$ sed '2,$s/dog/cat/' data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$
```

Because you may not know how many lines of data are in the text, the dollar sign often comes in handy.

### Using text pattern filters

The other method of restricting to which lines a command is applied is a bit more complicated. The sed editor allows the specification of a text pattern, and uses it as a filter to determine to which lines the command is applied. This is the format:

```
/pattern/command
```

You must encapsulate the *pattern* you specify in forward slashes. The sed editor applies the command only to lines that contain the text pattern you specify.

For example, if you want to change the default shell for only the user *rich*, you'd use the sed command:

```
$ grep /bin/bash /etc/passwd
root:x:0:0:root:/root:/bin/bash
christine:x:1001:1001::/home/christine:/bin/bash
rich:x:1002:1002::/home/rich:/bin/bash
$
```

```
$ sed '/rich/s/bash/csh/' /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
[...]
christine:x:1001:1001::/home/christine:/bin/bash
sshd:x:126:65534::/run/sshd:/usr/sbin/nologin
rich:x:1002:1002::/home/rich:/bin/csh
$
```
