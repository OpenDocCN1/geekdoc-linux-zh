# Chapter Seventeen: REGULAR EXPRESSION

A regular expression is a string that can be used to describe several sequences of characters. Regular expressions are used by several different Unix commands, including `ed`, `sed`, `awk`, `grep`, and, to a more limited extent, `vi`. Here `sed` stands for **stream editor** a stream oriented editor, which was created exclusively for executing scripts. Thus, all the input you feed into it passes through and goes to STDOUT and it does not change the input file.

# Invoking sed

Before we start, let us take make sure you have a local copy of `/etc/passwd` text file to work with `sed`. As mentioned previously, `sed` can be invoked by sending data through a pipe to it as follows –

```
```
$ cat /etc/passwd | sed
Usage: sed [OPTION]... {script-other-script} [input-file]...

-n, --quiet, --silent
                 suppress automatic printing of pattern space
-e script, --expression=script
                 "..." 
```

```

The `cat` command dumps the contents of `/etc/passwd` to `sed` through the pipe into `sed`'s pattern space. The pattern space is the internal work buffer that `sed` uses to do its work.

# The sed General Syntax

General syntax for sed

```
```
/pattern/action
```

```

Here, **pattern** is a regular expression, and **action** is one of the commands given in the following table. If **pattern** is omitted, **action** is performed for every line as we have seen above.

The slash characters ( / ) that surround the pattern are required because they are used as delimiters.

| Range | Description |
| :--- | :--- |
| P | Prints the line |
| D | Deletes the line |
| s/pattern1/pattern2/ | Substitutes the first occurrence of |