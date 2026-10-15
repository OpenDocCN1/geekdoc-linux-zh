
#!/bin/bash

function localizer {
    echo "==> In function localizer, a starts as '$a'"
    local a
    echo "==> After local declaration, a is '$a'"
    a="localizer version"
    echo "==> Leaving localizer, a is '$a'"
}

a="test"
echo "Before calling localizer, a is '$a'"
localizer
echo "After calling localizer, a is '$a'"

The log below demonstrates that the local version of $a within the localizer function shadows the global variable $a. The global $a is visible within localizer until the local declaration is encountered; local is in fact a command that creates the local variable at the point when it's executed.

```
$ sh scopetest.sh
Before calling localizer, a is 'test'
==> In function localizer, a starts as 'test'
==> After local declaration, a is ''
==> Leaving localizer, a is 'localizer version'
After calling localizer, a is 'test'
```

## Control flow

We've seen several if-then and if-then-else forms in this chapter already; they do exactly what you'd expect. The terminator for an if statement is fi. To chain your if clauses, you can use the elif keyword to mean "else if." For example:

```
if [ $base -eq 1 ] && [ $dm -eq 1 ]; then
    installDBase
elif [ $base -ne 1 ] && [ $dm -eq 1 ]; then
    installBase
elif [ $base -eq 1 ] && [ $dm -ne 1 ]; then
    installDM
else
    echo '===> Installing nothing'
fi
```

Both the peculiar [] syntax for comparisons and the command-line optionlike names of the integer comparison operators (e.g., -eq) are inherited from the original Bourne shell's channeling of /bin/test. The brackets are actually a shorthand way of invoking test and are not a syntactic requirement of the if statement.⁶

Table 2.2 shows the bash comparison operators for numbers and strings. bash uses textual operators for numbers and symbolic operators for strings, exactly the opposite of Perl.

## Table 2.2 Elementary bash comparison operators

| String | Numeric | True if |
|---|---|---|
| x = y | x -eq y | x is equal to y |
| x != y | x -ne y | x is not equal to y |
| x < y | x -lt y | x is less than y |
| x <= y | x -le y | x is less than or equal to y |
| x > y | x -gt y | x is greater than y |
| x >= y | x -ge y | x is greater than or equal to y |
| -n x | – | x is not null |
| -z x | – | x is null |

bash shines in its options for evaluating the properties of files (again, courtesy of its /bin/test legacy). Table 2.3 shows a few of bash's many file-testing and file-comparison operators.

## Table 2.3 bash file evaluation operators

| Operator | True if |
|---|---|
| -d file | file exists and is a directory |
| -e file | file exists |
| -f file | file exists and is a regular file |
| -r file | You have read permission on file |
| -s file | file exists and is not empty |
| -w file | You have write permission on file |
| file1 -nt file2 | file1 is newer than file2 |
| file1 -ot file2 | file1 is older than file2 |

Although the elif form is useful, a case selection is often a better choice for clarity. Its syntax is shown below in a sample routine that centralizes logging for a script. Of particular note are the closing parenthesis after each condition and the two semicolons that follow the statement block to be executed when a condition is met. The case statement ends with esac.

```
# The log level is set in the global variable LOG_LEVEL. The choices
# are, from most to least severe, Error, Warning, Info, and Debug.
function logMsg {
    message_level=$1
    message_itself=$2
```

```
if [ ${message_level} -le $LOG_LEVEL ]; then
  case ${message_level} in
    0) message_level_text="Error" ;;
    1) message_level_text="Warning" ;;
    2) message_level_text="Info" ;;
    3) message_level_text="Debug" ;;
    *) message_level_text="Other"
  esac
  echo "${message_level_text}: ${message_itself}"
fi
```

This routine illustrates the common “log level” paradigm used by many administrative applications. The code of the script generates messages at many different levels of detail, but only the ones that pass a globally set threshold, $LOG_LEVEL, are actually logged or acted upon. To clarify the importance of each message, the message text is preceded by a label that denotes its associated log level.

## Loops

bash’s for…in construct makes it easy to take some action for a group of values or files, especially when combined with filename globbing (the expansion of simple pattern-matching characters such as * and ? to form filenames or lists of filenames). The *.sh pattern in the for loop below returns a list of matching filenames in the current directory. The for statement then iterates through that list, assigning each filename in turn to the variable $file.

```
#!/bin/bash

suffix=BACKUP--`date +%Y%m%d-%H%M`

for script in *.sh; do
  newname="${script}.${suffix}"
  echo "Copying $script to $newname..."
  cp $script $newname
done
```

The output looks like this:

```
$ sh forex ample
Copying rhel.sh to rhel.sh.BACKUP--20091210-1708...
Copying sles.sh to sles.sh.BACKUP--20091210-1708...
...
```

The filename expansion is not magic in this context; it works exactly as it does on the command line. Which is to say, the expansion happens first and the line is then processed by the interpreter in its expanded form. You could just as well have entered the filenames statically, as in the line

```
for script in rhel.sh sles.sh; do
```

7. More accurately, the filename expansion is just a little bit magic in that it does maintain a notion of the atomicity of each filename. Filenames that contain spaces will go through the for loop in a single pass.
