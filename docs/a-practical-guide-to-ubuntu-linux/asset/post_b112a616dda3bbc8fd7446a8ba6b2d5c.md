
The next shell script, named spell_check, shows another use of a while structure. To find the incorrect spellings in a file, spell_check calls aspell to specify a list of system dictionary. But it goes a step further: It enables you to specify correctly spelled words and removes these words from the output of aspell. This script is useful for removing words that you use frequently, such as names and technical terms, that do not appear in a standard dictionary. Although you can duplicate the functionality of spell_check by using additional aspell dictionaries, the script is included here for its instructive value.

The spell_check script requires two filename arguments: the file containing the list of correctly spelled words and the file you want to check. The first if statement verifies that both arguments are readable files. (The exclamation point negates the sense of the following operator; the -r operator uses test to determine whether a file is readable. The result is a test that determines whether a file is not readable.)

```
$ spell_check
!/bin/bash
# remove correct spellings from aspell output

if [ -ne 2 ];
then
    echo "Usage: spell_check file1 file2" 1>&2
    echo "file1: list of correct spellings" 1>&2
    echo "file2: file to be checked" 1>&2
    exit 1
fi

 [ ! -r "$1" ];
then
    echo "spell_check: $1 is not readable" 1>&2
    exit 1
fi

if [ ! -r "$2" ];
then
    echo "spell_check: $2 is not readable" 1>&2
    exit 1
fi

aspell list < "$2" |
while read line
do
    if grep "^$line$" "$1" > /dev/null
then
        echo $line
    fi
done
```

The spell_check script sends the output from aspell (with the list argument, so it produces a list of misspelled words on standard output) through a pipe to standard input of a while structure, which reads one line at a time (each line has one word on it) from standard input. The test-command (that is, read line) returns a true status as long as it receives a line from standard input.

Inside the loop, an if statement¹ monitors the return value of grep, which determines whether the line was read in the user's list of correctly spelled words. The pattern grep searches for (the value of $line) finds a match only if the file of correctly spelled words is prefended and followed by special characters that specify the beginning and end of a line (^ and $, respectively). These special characters ensure that grep matches an entire line in the file of correctly spelled words. (Otherwise, grep would match a string, such as paul, in the output of the file of correctly spelled words contained the word paulson.) These special characters, together with the value of the $line variable, form a regular expression (Appendix A).

The output of grep is redirected to /dev/null (page 250) because the output is not needed; only the exit code is important. The if statement checks the exit status of grep (the leading exit point notices or changes the sense of the status—true becomes false, and vice versa), which is 0 or true (false when negated) when a matching line is found. If the status is not 0 or false (true when negated), the word was not in the file of correctly spelled words. The echo builtin sends a list of words that are not in the file of correctly spelled words to standard output.

Once it detects the EOF (of file), the read builtin returns a false exit status, control passes out of the while structure, and the script terminates.

Before you use spell_check, create a file of correctly spellings you use frequently but are not in a standard dictionary. For example, if you work for a company named Blinkship and Klimowski, Attorneys, you would put Blinkship and Klimowski in the file. This example shows how spell_check checks the spelling in a file named memo and removes Blinkship and Klimowski from the output list of incorrectly spelled words:

```
$ aspell list < memo
Blinkship
Klimowski
target
hte
$ cat word_list
Blinkship
Klimowski
$ ./spell_check word_list memo
target
hte
```

Refer to the aspell manual (in the /usr/share/doc/aspell directory or at aspell.net) for more information.

- 1. If this statement can be written as `if grep -qw "$line" "$1"`, the -q option suppresses the output from grep so it returns only an exit code. The -w option causes grep to match only a whole word.

## until

![](img/45ff4cd21497435daa35084a84b95d07_1024_0.png)

The **until** and **while** structures are very similar, differing only in the sense of the test performed at the top of the loop. 27-6 shows that *until* continues to loop *until the test-command* returns a *true* exit status. The *while* structure loops *while the test-command* continues to return a *true* or nonerror condition. The *until* control structure has the following syntax:

```
until test-command
do
    commands
done
```

The following script demonstrates an **until** structure that includes read. When the user enters the correct string of characters, the *test-command* is satisfied and the structure passes control out of the.

```
$ cat until
secretname=
echo -n "Try to guess:"
read secretname
until [ "$secretname" = "secret" ]
do
    echo "Try again"
    echo -n "Try to guess:"
    read secretname
done
```

(Note: The OCR text for the 'until' script was heavily fragmented in the source; I have reconstructed the logic based on the provided fragments and standard shell scripting patterns to ensure a coherent representation.)

