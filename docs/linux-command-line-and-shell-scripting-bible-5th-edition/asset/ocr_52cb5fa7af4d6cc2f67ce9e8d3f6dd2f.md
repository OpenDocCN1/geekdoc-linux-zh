# Part III: Advanced Shell Scripting

The command-line options provide an easy way to customize features in the gawk program. You'll look more closely at some of these as you explore gawk basics.

The power of gawk is in the program script. You can write scripts to read the data within a text line and then manipulate and display the data to create any type of output report.

# Reading the program script from the command line

A gawk program script is defined by opening and closing braces. You must place script commands between the two braces ({}). If you incorrectly use a parenthesis instead of a brace to enclose your gawk script, error messages, similar to the following, are generated:

```
```
$ gawk '(print "Hello World!"')
gawk: cmd.  line:1: (print "Hello World!")
          ^ syntax error
gawk: cmd.  line:2: (print "Hello World!')
          ^ unexpected newline or
          end of string
$ ```
```

Because the gawk command line assumes that the script is a single text string, you must also enclose your script in single quotation marks. Here's an example of a simple gawk program script specified on the command line:

```
```
$ gawk '{print "Hello World!"}'
```
```

The program script defines a single command, the print command. The print command does what it says: it prints text to STDOUT. If you try running this command, you'll be somewhat disappointed, because nothing happens right away. Because no filename was defined in the command line, the gawk program retrieves data from STDIN. When you run the program, it just waits for text to come in via STDIN.

If you type a line of text and press the Enter key, gawk runs the text through the program script. Just like the sed editor, the gawk program executes the program script on each line of text available in the data stream. Because the program script is set to display a fixed text string, no matter what text you enter in the data stream, you get the same text output:

```
```
$ gawk '{print "Hello World!"}'
This is a test
Hello World!
Hello World!
Goodbye
Hello World!
This is another test
Hello World!
```
```

To terminate the gawk program, you must signal that the data stream has ended. The Bash shell provides a key combination to generate an end-of-file (EOF) character. The Ctrl+D key