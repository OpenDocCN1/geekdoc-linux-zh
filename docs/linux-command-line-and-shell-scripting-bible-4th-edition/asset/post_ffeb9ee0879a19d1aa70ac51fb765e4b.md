
# Command substitution

One of the most useful features of shell scripts is the ability to extract information from the output of a command and assign it to a variable. Once you assign the output to a variable, you can use that value anywhere in your script. This comes in handy when you’re processing data in your scripts.

There are two ways to assign the output of a command to a variable:

- The backtick character
- The `$()` format

Be careful with the backtick character — it is not for the normal single quotation mark character you are used to using for strings. Because it is not used very often outside of shell scripts, you may not even know where to find it on your keyboard. You should become familiar with it, because it’s a crucial component of many shell scripts. Hint: On a U.S. keyboard, it is usually on the same key as the tilde symbol (~).

Command substitution allows you to assign the output of a shell command to a variable. Though this doesn’t seem like much, it is a major building block in script programming.

You must either surround the entire command-line command with the backtick characters:

```text
testing=`date`
```

or use the `$()` format:

```text
testing=$(date)
```

The shell runs the command within the command substitution characters and assigns the output to the variable `testing`. Notice that there aren't any spaces between the assignment equal sign and the command substitution character. Here's an example of creating a variable using the output from a normal shell command:

```bash
$ cat test5
#!/bin/bash
testing=$(date)
echo "The date and time are: " $testing
$
```

The variable testing receives the output from the date command, and it is used in the echo statement to display it. Running the shell script produces the following output:

```bash
$ chmod u+x test5
$ ./test5
The date and time are: Mon Jun 01 15:45:25 EDT 2020
$
```

That's not all that exciting in this example (you could just as easily put the command in the echo statement), but once you capture the command output in a variable, you can do anything with it.

Here's a popular example of how command substitution is employed to capture the current date and use it to create a unique filename in a script:

```bash
#!/bin/bash
# copy the /usr/bin directory listing to a log file
today=$(date +%y%m%d)
ls /usr/bin -al> log.$today
```

The today variable is assigned the output of a formatted date command. This is a common technique used to extract date information for log filenames. The +%y%m%d format instructs the date command to display the date as a two-digit year, month, and day:

```bash
$ date +%y%m%d
200601
$
```

The script assigns the value to a variable, which is then used as part of a filename. The file itself contains the redirected output (discussed later in the “Redirecting Input and Output” section) of a directory listing. After running the script, you should see a new file in your directory:

    -rw-r--r--    1 user     user        769 Jun 01 16:15
        log.200601

The log file appears in the directory using the value of the `$today` variable as part of the filename. The contents of the log file are the directory listing from the /usr/bin directory. If the script is run the next day, the log filename will be log.200602 , thus creating a new file for the new day.

**WARNING**

Command substitution creates what's called a subshell to run the enclosed command. A subshell is a separate child shell generated from the shell that's running the script. Because of that, any variables that you create in the script won't be available to commands running in the subshell.

Subshells are also created if you run a command from the command prompt using the ./ path, but they aren't created if you just run the command without a path. However, if you use a built-in shell command, that doesn't generate a subshell. Be careful when running scripts from the command prompt!

# Redirecting Input and Output

There are times when you'd like to save the output from a command instead of just having it displayed on the monitor. The Bash shell provides a few different operators that allow you to redirect the output of a command to an alternative location (such as a file). Redirection can be used for input as well as output, redirecting a file to a command for input. This section describes what you need to do to use redirection in your shell scripts.

## Output redirection

The most basic type of redirection is sending output from a command to a file. The Bash shell uses the greater-than symbol (>) for this:

```text
command> outfile
```

Anything that would appear on the monitor from the command instead is stored in the output file specified:

```bash
$ date> test6
$ ls -l test6
-rw-r--r-- 1 user user 29 Jun 01 16:56 test6
$ cat test6
Mon Jun 01 16:56:58 EDT 2020
$
```

The redirect operator created the file test6 (using the default umask settings) and redirected the output from the date command to the test6 file. If the output file already exists, the redirect operator overwrites the existing file with the new file data:

```bash
$ who> test6
$ cat test6
rich pts/0 Jun 01 16:55
$
```

Now the contents of the test6 file contain the output from the who command.

Sometimes, instead of overwriting the file’s contents, you may need to append output from a command to an existing file — for example, if you’re creating a log file to document an action on the system. In this situation, you can use the double greater-than symbol (>>) to append data:

```bash
$ date>> test6
$ cat test6
rich pts/0 Jun 01 16:55
Mon Jun 01 17:02:14 EDT 2020
$
```

The test6 file still contains the original data from the who command processed earlier — plus now it contains the new output from the date command.

## Input redirection

Input redirection is the opposite of output redirection. Instead of taking the output of a command and redirecting it to a file, input redirection takes the content of a file and redirects it to a command. The input redirection symbol is the less-than symbol (<):

```text
command < inputfile
```

The easy way to remember this is that the command is always listed first in the command line, and the redirection symbol “points” to the way the data is flowing. The less-than symbol indicates that the data is flowing from the input file to the command.

Here’s an example of using input redirection with the `wc` command:

```bash
$ wc < test6
2       11       60
$
```

The `wc` command provides a count of text in the data. By default, it produces three values:

- The number of lines in the text
- The number of words in the text
- The number of bytes in the text

By redirecting a text file to the `wc` command, you can get a quick count of the lines, words, and bytes in the file. The example shows that there are 2 lines, 11 words, and 60 bytes in the test6 file.

There’s another method of input redirection, called *inline input redirection*. This method allows you to specify the data for input redirection on the command line instead of in a file. This may seem somewhat odd at first, but there are a few applications for this process (such as those shown in the “Performing Math” section later).

The inline input redirection symbol is the double less-than symbol (<<). Besides this symbol, you must specify a text marker that delineates the beginning and end of the data used for input. You can use any string value for the text marker, but it must be the same at the beginning of the data and the end of the data:

```text
command << marker
```
