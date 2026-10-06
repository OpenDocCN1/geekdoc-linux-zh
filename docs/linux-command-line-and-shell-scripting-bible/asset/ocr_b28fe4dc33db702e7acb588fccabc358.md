# Part III Advanced Shell Scripting

| TABLE 16-2 | |
| Option | Description |
| - | - |
| -F fs | Specify a file separator for delineating data fields in a line. |
| -f file | Specify a filename to read the program. |
| -v var=value | Define a variable and default value used in the gawk program. |
| -mf N | Specify the maximum number of fields to process in the data file. |
| -mr N | Specify the maximum record size in the data file. |
| -W keyword | Specify the compatibility mode or warning level for gawk. |

# ### Reading the program script from the command line

A awk program script is defined by opening and closing braces. You must place script commands between the two braces. Since the gawk command line assumes that the script is a single text string, you must also include your script in single quotation marks. Here's an example of a simple awk program script specified on the command line:

```
$ gawk '[print "Hello John!\']'
```

The program script defines a single command, the print command. The print command does what it says, it prints text to STDOUT. If you try running this command, you will be disappointed, and nothing will happen right away. Since no filename was defined in the command line, the gawk retrieves data from STDIN. When you run the program, it waits for text to come in via STDIN.

If you type a line of text and press the Enter key, gawk will run the text through the program script:

```
$ gawk '[print "Hello World!\']'
This is a test
Hello John!
hello
Hello John!
This is another test
Hello John!
$
```

Just like the sed editor, the gawk program executes the program script on each line of text available in the data stream. Since the program script is set to display a fixed text string, no matter what text you enter in the data stream, you'll get the same text output.

424