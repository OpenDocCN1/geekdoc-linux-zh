
# EXAMPLE 4.26

```
% grep -c 'west' datafile
3
```

## EXPLANATION

The -c option causes grep to print the number of lines where the pattern was found. This does not mean the number of occurrences of the pattern. For example, if west is found three times on a line, it only counts the line once.

# EXAMPLE 4.27

```
% grep -w 'north' datafile
north    NO    Margot Weber    4.5    .89    5    9
```

## EXPLANATION

The -w option causes grep to find the pattern only if it is a word, not part of a word. Only the line containing the word north is printed, not northwest, northeast, etc.

a. A word is a sequence of alphanumeric characters starting at the beginning of a line or preceded by whitespace and ending in whitespace, punctuation, or a newline.

# EXAMPLE 4.28

```
% echo $LOGNAME
lewis

% grep -i "$LOGNAME" datafile
southwest    SW    Lewis Dalsass    2.7    .8    2    18
```

## EXPLANATION

The value of the shell ENV variable, LOGNAME, is printed. It contains the user's login name. If the variable is enclosed in double quotes, it will still be expanded by the shell, and in case there is more than one word assigned to the variable, whitespace is shielded from shell interpretation. If single quotes are used, variable substitution does not take place; that is, $LOGNAME is printed.

## 4.4 grep with Pipes

Instead of taking its input from a file, grep often gets its input from a pipe.

# EXAMPLE 4.29

```
% ls -l
drwxrwxrwx 2 ellie 2441 Jan 6 12:34 dir1
-rw-r--r-- 1 ellie 1538 Jan 2 15:50 file1
-rw-r--r-- 1 ellie 1539 Jan 3 13:36 file2
-rw-r--r-- 2 ellie 2341 Jan 6 12:34 grades

% ls -l | grep '^d'
drwxrwxrwx 2 ellie 2441 Jan 6 12:34 dir1
drwxrwxrwx 2 ellie 2341 Jan 6 12:34 grades
```

## EXPLANATION

The output of the ls command is piped to grep. All lines of output that begin with a d are printed; that is, all directories are printed.

### 4.4.1 grep Review

Table 4.3 contains examples of grep commands and what they do.

## Table 4.3 Review of grep

| Command | What It Does |
|---|---|
| grep '\<Tom\>' file | Prints lines containing the word Tom. |
| grep 'Tom Savage' file | Prints lines containing Tom Savage. |
| grep '^Tommy' file | Prints lines if Tommy is at the beginning of the line. |
| grep '\.bak$' file | Prints lines ending in .bak. Single quotes protect the dollar sign ($) from interpretation. |
| grep '[Pp]yramid' * | Prints lines from all files containing pyramid or Pyramid in the current working directory. |
| grep '[A-Z]' file | Prints lines containing at least one capital letter. |
| grep '[0-9]' file | Prints lines containing at least one number. |
| grep '[A-Z][...][0-9]' file | Prints lines containing five-character patterns starting with a capital letter and ending with a number. |
| grep -w '[Tt]est' files | Prints lines with the word Test and/or test. |

## Table 4.3 Review of grep (continued)

| Command | What It Does |
|---|---|
| grep -s 'Mark Todd' file | Finds lines containing Mark Todd, but does not print the lines. Can be used when checking grep's exit status. |
| grep -v 'Mary' file | Prints all lines not containing Mary. |
| grep -i 'sam' file | Prints all lines containing sam, regardless of case (e.g., SAM, sam, SaM, sAm). |
| grep -l 'Dear Boss' * | Lists all filenames containing Dear Boss. |
| grep -n 'Tom' file | Precedes matching lines with line numbers. |
| grep "$name" file | Expands the value of variable name and prints lines containing that value. Must use double quotes. |
| grep '\$5' file | Prints lines containing literal $5. Must use single quotes. |
| ps -ef | grep '^ *user1' | Pipes output of ps -ef to grep, searching for user1 at the beginning of a line, even if it is preceded by zero or more spaces. |

## 4.5 egrep (Extended grep)

The main advantage of using egrep is that additional regular expression metacharacters (see Table 4.4) have been added to the set provided by grep. The \( \) and \{ \}, however, are not allowed. (See GNU grep -E if using Linux.)

## Table 4.4 egrep's Regular Expression Metacharacters

| Metacharacter | Function | Example | What It Matches |
|---|---|---|---|
| ^ | Beginning-of-line anchor | '^love' | Matches all lines beginning with love. |
| $ | End-of-line anchor | 'love$' | Matches all lines ending with love. |
| . | Matches one character | 'l..e' | Matches lines containing an l, followed by two characters, followed by an e. |
| * | Matches zero or more of the characters preceding the asterisk | '.* love' | Matches lines with zero or more spaces followed by the pattern love. |
| [ ] | Matches one character in the set | '[Ll]ove' | Matches lines containing love or Love. |
