
UNIX power users have a long tradition of using the right tool for the right job and you can never have enough tricks in your bag. sed isn’t the right tool for writing a résumé or even a letter to your Aunt Hortense. However, it simply can’t be beat when you need to change every pipe character to a colon in a dozen different files and then send those files to another program for processing.

## How does it work?

sed reads a set of characters, a stream, from stdin and writes to stdout. It can be given a series of operations to perform on the command line, if they are short, or it can read a set of instructions from a script file. A common invocation might look something like this:

```
sed -e '{some sed command}' input_file > output_file
```

or alternatively, if reading a set of commands from a script file, it might look similar to this:

```
sed -f {script file} input_file > output_file
```

Unless you specify otherwise, sed will apply the commands you enter to every line in the input stream. You can limit the lines that get affected in various ways such as specifying beginning and ending line numbers or even start or end blocks by pattern matches. These affected lines are normally referred to as addresses, and these addresses can be specified as either zero, one, or two addresses. Addresses can be any combination of either patterns (which are enclosed in slashes), line numbers, or line specifier symbols.

Commands are extensive and varied. Some of these include:

- = Print the line number of the line to stdout
- s Perform a substitution on the address
- d Delete the addressed lines
- w Write the addressed lines to a file
- q Quit when the address is encountered

There are many more commands available, but this list should give you a small taste of what sed can do.

## Can you give me some examples of how to use sed?

By combining both addresses and commands, you form a complete sed command, which might look something like this:

```
sed -e '/foo/d' myfile
```

This sed invocation would delete every line that contains the word "foo" and print the results to standard out. This is an example of using zero addresses, which results in attempting the match on every single line. Another example would be:

```
sed -e '50d' myfile
```

which would result in deleting line 50 of myfile, while

```
sed -e '50,$d' myfile
```

would delete everything from line 50 to the end ($ refers to the last line in the stream). Another common task involves replacing one pattern of text with another. This is done using the s command, instead of the d above, and might look similar to the following:

```
sed -e 's/foo/bar/' myfile
```

This example would substitute the first occurrence of the word "foo" with the word "bar" on each line. If you wanted to replace multiple occurrences on the same line, you would need to append a g after the command, as in the following:

```
sed -e 's/foo/bar/g' myfile
```

Regular expression patterns can be used in the search space above (instead of "foo", for example), which can add more power to your editing. If you wanted to place a series of asterisks in front of specific lines, for example, you might use:

```
sed -e '/foo/s/^/*** /' myfile
```

This would find every line with the word "foo" in it, and replace the beginning of the line (^ is a special symbol that refers to the beginning of the line) with three asterisks.

A final word of warning is in order. Since sed is stream-oriented, it does not read the entire input file into memory before it opens the output stream. This means that if you try to edit a file in place with something like this:

```
sed -e 's/foo/bar/' myfile > myfile   # THIS IS WRONG
```

you will end up with a zero byte file and a very silly look on your face.

## Appendix A

## Command Reference

![](img/0c1fc10350aa06ca92e7921c96c628ec_281_0.png)

Of course you know that there are hundreds of commands in the various versions of UNIX, so you won’t find all of them here. But you will find a lot of very useful ones—especially the ones used for the tricks in this book. We’ll show you the syntax and available options and a little on how each command works.

Because there are variations among the flavors of UNIX, your version may have slightly different syntax and/or options than the ones shown here. If you see a command that looks like it might do what you want to do but you don’t see exactly the right option or you get a syntax error upon execution, check your documentation for possible variations.

### alias [options] name[=‘cmd’]

#### OBJECTIVE:

Assigns a shorthand name to substitute for cmd. If ‘cmd’ is omitted, it prints the alias for name. Korn shell only.

#### OPTIONS AND VARIABLES

- -t Creates a tracked alias for a UNIX command. The shell will remember the full path name of the command, making it easier to find.
- -x Exports the alias so it can be used in shell scripts.

### at options time [date] [+increment]

#### OBJECTIVE:

Lets you schedule jobs to be executed later.

#### OPTIONS AND VARIABLES

- -l [jobID] Lists your currently scheduled jobs. Include a jobID if you want information on just one job.
- -r [jobID] Removes specified job from the queue. You can remove only your own jobs unless you’re the superuser.
- time Specifies the time the job should start. The format is hh:mm [modifiers]. A 24-hour clock is assumed unless you add the modifier am or pm, in which case time is based on a 23-hour clock.
