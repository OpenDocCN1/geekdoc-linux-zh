
## Table 13.10 Metacharacters (continued)

| Metacharacter | Meaning |
|---|---|
| [abc] | Matches for one character from a set of characters; for example, a, b, or c |
| [!abc] | Matches for one character not from the set of characters; for example, not a, b, or c |
| * | Matches for zero or more characters |
| (cmds) | Executes commands in a subshell |
| {cmds} | Executes commands in current shell |

## 13.9 Filename Substitution (Globbing)

When evaluating the command line, the shell uses metacharacters to abbreviate filenames or pathnames that match a certain set of characters. The filename substitution metacharacters listed in Table 13.11 are expanded into an alphabetically listed set of filenames. The process of expanding the metacharacter into filenames is also called filename substitution, or globbing. If a metacharacter is used and there is no filename that matches it, the shell treats the metacharacter as a literal character.

## Table 13.11 Shell Metacharacters and Filename Substitution

| Metacharacter | Meaning |
|---|---|
| * | Matches zero or more characters |
| ? | Matches exactly one character |
| [abc] | Matches one character in the set a, b, or c |
| [!abc] | Matches one character not in the set, not a, b, or c |
| {a,i le,ax} | Matches for a character or set of characters |
| [a-z] | Matches for one character in the range from a to z |
| [!a-z] | Matches one character not in the range from a to z |
| \ | Escapes or disables the metacharacter |

### 13.9.1 The Asterisk

The asterisk is a wildcard that matches for zero or more of any characters in a filename.

## EXAMPLE 13.41

```
1  $ ls *
abc abc1 abc122 abc123 abc2 file1 file1.bak file2 file2.bak none
nonsense nobody nothing nowhere one
2  $ ls *.bak
file1.bak file2.bak
3  $ echo a*
ab abc1 abc122 abc123 abc2
```

## EXPLANATION

- 1 The asterisk expands to all of the files in the present working directory. All of the files are passed as arguments to ls and displayed.
- 2 All files starting with zero or more characters and ending with .bak are matched and listed.
- 3 All files starting with a, followed by zero or more characters, are matched and passed as arguments to the echo command.

### 13.9.2 The Question Mark

The question mark represents a single character in a filename. When a filename contains one or more question marks, the shell performs filename substitution by replacing the question mark with the character it matches in the filename.

## EXAMPLE 13.42

```
1  $ ls
abc abc122 abc2 file1.bak file2.bak nonsense nothing one
abc1 abc123 file1 file2 none noone nowhere
2  $ ls a?c?
abc1 abc2
3  $ ls ??
ls: ??: No such file or directory
4  $ echo abc???
abc122 abc123
5  $ echo ??
??
```

## EXPLANATION

- 1 The files in the current directory are listed.
- 2 Filenames starting with a, followed by a single character, followed by c and a single character, are matched and listed.
- 3 Filenames containing exactly two characters are listed, if found. Because there are not any two-character files, the question marks are treated as a literal filename. Such a file is not found, and the error message is printed.

## EXPLANATION (CONTINUED)

- 4 Filenames starting with abc and followed by exactly three characters are expanded and displayed by the echo command.
- 5 There are no files in the directory that contain exactly two characters. The shell treats the question mark as a literal question mark if it cannot find a match.

### 13.9.3 The Square Brackets

The brackets are used to match filenames containing one character in a set or range of characters.

## EXAMPLE 13.43

```
1 $ ls
abc abc122 abc2 file1.bak file2.bak nonsense nothing
one abc1 abc123 file1 file2 none noone nowhere
2 $ ls abc[123]
abc1 abc2
3 $ ls abc[1-3]
abc1 abc2
4 $ ls [a-z][a-z][a-z]
abc one
5 $ ls [!f-z]???
abc1 abc2
6 $ ls abc12[23]
abc122 abc123
```

## EXPLANATION

- 1 All of the files in the present working directory are listed.
- 2 All filenames containing four characters are matched and listed if the filename starts with abc, followed by 1, 2, or 3. Only one character from the set in the brackets is matched.
- 3 All filenames containing four characters are matched and listed, if the filename starts with abc and is followed by a number in the range from 1 to 3.
- 4 All filenames containing three characters are matched and listed, if the filename starts with abc and contains exactly three lowercase alphabetic characters.
- 5 All filenames containing four characters are listed if the first character is not a letter between f and z [!f-z], followed by three of any characters, where ? represents a single character.
- 6 Files are listed if the filenames contain abc12 followed by 2 or 3.
