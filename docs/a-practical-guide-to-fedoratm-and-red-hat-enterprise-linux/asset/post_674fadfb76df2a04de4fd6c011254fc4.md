
```bash
$ cat for_test
for arg
do
echo "$arg"
done

$ for_test candy gum chocolate
candy
gum
chocolate
```

The next example uses a different syntax. In it, the *loop-index* is named *count* and is set to an initial value of 0. The condition to be tested is *count<=10*; **bash** continues executing the loop as long as this condition is *true* (as long as *count* is less than or equal to 10; see Table 27-8 on page 1059 for a list of operators). Each pass through the loop, **bash** adds 2 to the value of *count* (*count+=2*).

```bash
$ cat step2
for (( count=0; count<=10; count+=2 ))
do
echo -n "$count "
done
echo

$ ./step2
0 2 4 6 8 10
```

## The whos Script

The following script, named **whos**, demonstrates the usefulness of the implied *"$@"* in the *for* structure. You give **whos** one or more users' full names or user-names as arguments, and **whos** displays information about the users. The **whos** script gets the information it displays from the first and fifth fields in the */etc/passwd* file. The first field contains a username, and the fifth field typically contains the user's full name. You can provide a username as an argument to **whos** to display the user's name or provide a name as an argument to display the username. The **whos** script is similar to the *finger* utility, although **whos** delivers less information.

```bash
$ cat whos
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Usage: whos id..." 1>&2
    exit 1
fi

for id
do
    gawk '-F: '{print $1, $5}' /etc/passwd |
    grep -i "$id"
done
```

In the next example, whois identifies the user whose username is chas and the user whose name is Marilou Smith:

```bash
$ whois chas "Marilou Smith"
chas Charles Casey
msmith Marilou Smith
```

The who script uses a for statement to loop through the command-line arguments. In this script the implied use of "$@" in the for loop is particularly beneficial because it causes the for loop to treat an argument that contains a SPACE as a single argument. This example encloses Marilou Smith in quotation marks, which causes the shell to pass it to the script as a single argument. Then the implied "$@" in the for statement causes the shell to regenerate the quoted argument Marilou Smith so that it is again treated as a single argument. The double quotation marks in the grep statement perform the same function.

For each command-line argument, whois searches the /etc/passwd file. Inside the for loop, the gawk utility extracts the first ($1) and fifth ($5) fields from each line in /etc/passwd. The `-F:` option causes gawk to use a colon (:) as a field separator when it reads /etc/passwd, allowing it to break each line into fields. The gawk command sets and uses the $1 and $5 arguments; they are included within single quotation marks and are not interpreted by the shell. Do not confuse these arguments with positional parameters, which correspond to command-line arguments. The first and fifth fields are sent to grep (page 232) via a pipeline. The grep utility searches for $id (to which the shell has assigned the value of a command-line argument) in its input. The `-i` option causes grep to ignore case as it searches; grep displays each line in its input that contains $id.

Under bash, a control operator such as a pipeline symbol (|) implies continuation: bash "knows" another command must follow it. Therefore, in whois, the TERMULUE following the pipeline symbol at the end of the line with the gawk command does not have to be quoted. For more information refer to "Implicit Command-Line Continuation" on page 1063.

## while

The while control structure has the following syntax:

```bash
while test-command
do
    commands
done
```

![](img/243613168ac865b539f12460d966088e_1056_0.png)

### Figure 27-5 A while flowchart

As long as the *test-command* (Figure 27-5) returns a *true* exit status, the *while* structure continues to execute the series of *commands* delimited by the *do* and *done* statements. Before each loop through the *commands*, the structure executes the *test-command*. When the exit status of the *test-command* is *false*, the structure passes control to the statement after the *done* statement.

## test builtin

The following shell script first initializes the *number* variable to zero. The *test* builtin then determines whether *number* is less than 10. The script uses *test* with the **-lt** argument to perform a numerical test. For numerical comparisons, you must use **-ne** (not equal), **-eq** (equal), **-gt** (greater than), **-ge** (greater than or equal to), **-lt** (less than), or **-le** (less than or equal to). For string comparisons, *use* (= equal) or **!=** (not equal) when you are working with *test*. In this example, *test* has an exit status of 0 (*true*) as long as *number* is less than 10. As long as *test* returns *true*, the structure executes the commands between the *do* and *done* statements. See page 983 for information on the *test* builtin.

```bash
$ cat count
#!/bin/bash
number=0
while [ "$number" -lt 10 ]
do
    echo -n "$number"
    ((number +=1))
done

echo
$ ./count
0123456789
$
```

The *echo* command following *do* displays *number*. The **-n** prevents *echo* from issuing a *NEWLINE* following its output. The next command uses arithmetic evaluation ((...)); page 1056] to increment the value of *number* by 1. The *done* statement terminates the loop and returns control to the *while* statement to start the loop over again. The final *echo* causes *count* to send a *NEWLINE* character to standard output, so the next prompt is displayed at the left edge of the display rather than immediately following the 9.

## The spell_check Script

The **aspell** utility (**aspell** package) checks the words in a file against a dictionary of correctly spelled words. With the **list** command, **aspell** runs in list mode: Input comes from standard input and **aspell** sends each potentially misspelled word to standard output. The following command produces a list of possible misspellings in the file letter.txt:

```bash
$ aspell list < letter.txt
quikly
portible
frendly
```

The next shell script, named **spell_check**, shows another use of a **while** structure. To find the incorrect spellings in a file, **spell_check** calls **aspell** to check a file against a system dictionary. But it goes a step further: It enables you to specify a list of correctly spelled words and removes these words from the output of **aspell**. This script is useful for removing words you use frequently, such as names and technical terms, that do not appear in a standard dictionary. Although you can duplicate the functionality of **spell_check** by using additional **aspell** dictionaries, the script is included here for its instructive value.

The **spell_check** script requires two filename arguments: the file containing the list of correctly spelled words and the file you want to check. The first if statement verifies that the user specified two arguments. The next two if statements verify that both arguments are readable files. The logical expansion point negates the sense of the following operator; the `-r` operator causes **test** to determine whether a file is readable. The result is a test that determines whether a file is *not readable*.

```bash
$ cat spell_check
#!/bin/bash
# remove correct spellings from aspell output

if [ $# -ne 2 ]
then
    echo "Usage: spell_check dictionary filename" 1>&2
    echo "dictionary: list of correct spellings" 1>&2
    echo "filename: file to be checked" 1>&2
    exit 1
fi

if [ ! -r "$1" ]
then
    echo "spell_check: $1 is not readable" 1>&2
    exit 1
fi

if [ ! -r "$2" ]
then
    echo "spell_check: $2 is not readable" 1>&2
    exit 1
fi

aspell list < "$2" |
while read line
do
    if ! grep "^\$line$" "$1" > /dev/null
    then
        echo $line
    fi
done
```

The spell_check script sends the output from aspell (with the list argument, so it produces a list of misspelled words on standard output) through a pipeline to standard input of a while structure, which reads one line at a time (each line has one word on it) from standard input. The test-command (that is, read line) returns a true exit status as long as it receives a line from standard input.

Inside the while loop, an if statement monitors the return value of grep, which determines whether the line that was read is in the user's list of correctly spelled words. The pattern grep searches for (the value of $line) is preceded and followed by special characters that specify the beginning and end of a line (^ and $, respectively). These special characters ensure that grep finds a match only if the $line variable matches an entire line in the file of correctly spelled words. (Otherwise, grep would match a string, such as paul, in the output of aspell if the file of correctly spelled words contained the word paulson.) These special characters, together with the value of the $line variable, form a regular expression (Appendix A).

The output of grep is redirected to /dev/null (page 158) because the output is not needed; only the exit code is important. The if statement checks the negated exit status of grep (the leading exclamation point negates or changes the sense of the exit status—true becomes false, and vice versa), which is 0 or true (false when negated) when a matching line is found. If the exit status is not 0 or false (true when negated), the word was not in the file of correctly spelled words. The echo builtin sends a list of words that are not in the file of correctly spelled words to standard output.

Once it detects the EOF (end of file), the read builtin returns a false exit status, control passes out of the while structure, and the script terminates.

Before you use spell_check, create a file of correct spellings containing words that you use frequently but that are not in a standard dictionary. For example, if you work for a company named Blinkenship and Kilmowski, Attorneyes, you would put Blinkenship and Kilmowski in the file. The following example shows how spell_check checks the spelling in a file named memo and removes Blinkenship and Kilmowski from the output list of incorrectly spelled words:

```bash
$ aspell list < memo
Blinkenship
Kilmowski
target
hte
$ cat word_list
Blinkenship
Kilmowski
$ ./spell_check word_list memo
target
hte
```

Refer to /usr/share/doc/aspell or aspell.net for more information.
