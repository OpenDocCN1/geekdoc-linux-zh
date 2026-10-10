
## Defining an editor command in the command line

| Option | Description |
|---|---|
| -e commands | Adds additional sed commands to run while processing the input |
| -f file | Adds the commands specified in the file to the commands run while processing the input |
| -n | Doesn't produce output for each command, but waits for the print (p) command |

The script parameter specifies a single command to apply against the data stream. If more than one command is required, you must use either the -e option to specify them in the command line or the -f option to specify them in a separate file. Numerous commands are available for manipulating data. We examine some of the basic commands used by the sed editor in this chapter and then look at some of the more advanced commands in Chapter 21, “Advanced sed.”

By default, the sed editor applies the specified commands to the STDIN input stream. This allows you to pipe data directly to the sed editor for processing. Here’s a quick example demonstrating how to do this:

```
$ echo "This is a test" | sed 's/test/big test/'
This is a big test
$
```

This example uses the s command in the sed editor. The s command substitutes a second text string for the first text string pattern specified between the forward slashes. In this example, the words big test were substituted for the word test.

When you run this example, it should display the results almost instantaneously. That’s the power of using the sed editor. You can make multiple edits to data in about the same time it takes for some of the interactive editors just to start up!

Of course, this simple test demonstrated an edit of one data line. The same speedy results occur when editing complete files of data, as shown here:

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$ sed 's/dog/cat/' data1.txt
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$
```

The sed command executes and returns the data very quickly. As it processes each line of data, the results are displayed. You'll start seeing results before the sed editor completes processing the entire file.

It's important to note that the sed editor *doesn't* modify the data in the text file itself; it only sends the modified text to `STDOUT`. If you look at the text file, it still contains the original data:

```
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
```

### Using multiple editor commands in the command line

To execute more than one command from the sed command line, use the -e option:

```
$ sed -e 's/brown/red/; s/dog/cat/' data1.txt
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
$
```

Both commands are applied to each line of data in the file. The commands must be separated with a semicolon (;), and there shouldn't be any spaces between the end of the first command and the semicolon.

Instead of using a semicolon to separate the commands, you can use the secondary prompt in the Bash shell. Just enter the first single quotation mark to open the sed program script (also called the sed editor command list), and Bash continues to prompt you for more commands until you enter the closing quotation mark:

```
$ sed -e '
> s/brown/green/
> s/fox/toad/
> s/dog/cat/' data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
$ 
```

You must remember to finish the command on the same line where the closing single quotation mark appears. After the Bash shell detects the closing quotation mark, it processes the command. After it starts, the sed command applies each command you specified to each data line in the text file.

### Reading editor commands from a file

Finally, if you have lots of sed commands you want to process, it is often easier to just store them in a separate file. Use the -f option to specify the file in the sed command:

```
$ cat script1.sed
s/brown/green/
s/fox/toad/
s/dog/cat/
$ 
$ sed -f script1.sed data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
$ 
```

In this case, a semicolon is *not* placed after each command. The sed editor knows that each line contains a separate command. As with entering commands on the command line, the sed editor reads the commands from the specified file and applies them to each line in the data file.

**TIP**  
*It’s easy to confuse sed editor script files with Bash shell scripts or other text files. To eliminate confusion, it is considered good form to use the .sed file extension on any sed script files.*

We’ll look at some other *sed* editor commands that come in handy for manipulating data in the “Looking at the *sed* Editor Basic Commands” section. Before that, let’s quickly look at the other Linux data editor.

## Getting to know the *gawk* program

Although the *sed* editor is a handy tool for modifying text files on the fly, it has its limitations. Often, a more advanced tool is needed for manipulating data in a file, one that provides a more programming-like environment allowing the modification and reorganization of data in a file. This is where *gawk* comes in.

**NOTE**  
*The gawk program is not installed by default on all distributions. If your Linux distribution does not have the gawk program, install the gawk package using Chapter 9, “Installing Software,” as a guide.*

The *gawk* program is the GNU version of the original *awk* program in Unix. The *gawk* program takes stream editing one step further than the *sed* editor by providing a programming language instead of just editor commands. Within the *gawk* programming language, the following is possible:

- Define variables to store data.
- Use arithmetic and string operators to operate on data.
- Use structured programming concepts, such as *if-then* statements and loops, to add logic to your data processing.
- Generate formatted reports by extracting data elements within the data file and repositioning them in another order or format.

The *gawk* program's report-generating capabilities are often used for extracting data elements from large, bulky text files and formatting them into a readable report. The perfect example of this is formatting program log files. Trying to dig through lines of errors in a log file can be difficult. The *gawk* program allows the filtering of data elements you want to view from the log file, and then formats them in a manner that makes reading the important data easier.

### Visiting the *gawk* command format

Here's the basic format of the *gawk* program:

```
*gawk* options program file
```

Table 19.2 shows a few options available with the *gawk* program.

**TABLE 19.2 The *gawk* Options**

| Option | Description |
|---|---|
| -F fs | Specifies a file separator for delineating data fields in a line |
| -f file | Specifies a filename to read the program from |
| -v var = value | Defines a variable and default value used in the *gawk* program |
| -L [ keyword ] | Specifies the compatibility mode or warning level for *gawk* |

The command-line options provide an easy way to customize features in the *gawk* program. We'll look more closely at some of these as we explore *gawk* basics.

The power of *gawk* is in the program script. You can write scripts to read the data within a text line and then manipulate and display the
