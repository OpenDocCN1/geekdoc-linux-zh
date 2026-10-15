
## 9.8 Filename Substitution

Table 9.3 Shell Metacharacters (continued)

| Metacharacter | Purpose | Example | Meaning |
|---|---|---|---|
| ( ) | Groups commands to be executed in a subshell | {ls ; pwd} >tmp | Executes commands and sends output to tmp file. |
| { } | Groups commands to be executed in this shell | { cd /; echo $cwd } | Changes to root directory and displays current working directory. |

When evaluating the command line, the shell uses metacharacters to abbreviate filenames or pathnames that match a certain set of characters. The filename substitution metacharacters listed in Table 9.4 are expanded into an alphabetically listed set of filenames. The process of expanding a metacharacter into filenames is also called globbing. Unlike the other shells, when the C shell cannot substitute a filename for the metacharacter it is supposed to represent, the shell reports No match.

Table 9.4 Shell Metacharacters and Filename Substitution

| Metacharacter | Meaning |
|---|---|
| * | Matches zero or more characters |
| ? | Matches exactly one character |
| [abc] | Matches one character in the set: a, b, or c |
| [a-z] | Matches one character in the range a to z |
| {a, !le, ax} | Matches for a character or set of characters |
| ~ | Substitutes the user's home directory for tilde |
| \ | Escapes or disables the metacharacter |

The shell performs filename substitution by evaluating its metacharacters and replacing them with the appropriate letters or digits in a filename.

### 9.8.1 The Asterisk

The asterisk matches zero or more characters in a filename.

# EXAMPLE 9.28

```
1 % ls
 a.c b.c abc ab3 file1 file2 file3 file4 file5
2 % echo *
 a.c b.c abc ab3 file1 file2 file3 file4 file5
3 % ls *.c
 a.c b.c
4 % rm z?p
 No match.
```

# EXPLANATION

- 1 All the files in the current directory are listed.
- 2 The echo program prints all its arguments to the screen. The asterisk (also called a splat) is a wildcard that means: match for zero or more of any characters found in a filename. All the files in the directory are matched and echoed to the screen.
- 3 Filenames ending in .c are listed.
- 4 Because none of the files in the directory start with z, the shell reports No match.

### 9.8.2 The Question Mark

The question mark matches exactly one character in a filename.

# EXAMPLE 9.29

```
1 % ls
 a.c b.c abc ab3 file1 file2 file3 file4 file5
2 % ls ???
 abc ab3
3 % echo How are you?
 No match.
4 % echo How are you\?
 How are you?
```

# EXPLANATION

- 1 All the files in the current directory are listed.
- 2 The question mark matches for a single-character filename. Any filenames consisting of three characters are listed.
- 3 The shell looks for a filename spelled y-o-u followed by one character. There is not a file in the directory that matches these characters. The shell prints No match.
- 4 The backslash preceding the question mark is used to turn off the special meaning of the question mark. Now the shell treats the question mark as a literal character.

### 9.8.3 The Square Brackets

The square brackets match a filename for one character from a set or range of characters.

# EXAMPLE 9.30

```
1 % ls
a.c b.c abc ab3 file1 file2 file3 file4 file5 file10 file11 file12
2 % ls file[123]
file1 file2 file3
3 % ls [A-Za-z][a-z][1-5]
ab3
4 % ls file[0-2]
file10 file11 file12
```

# EXPLANATION

- 1 All the files in the current directory are listed.
- 2 Filenames starting with file and followed by a 1, 2, or 3 are matched and listed.
- 3 Filenames starting with a letter (either uppercase or lowercase) followed by a lowercase letter, and followed by a number between 1 and 5 are matched and listed.
- 4 Filenames starting with file1 and followed by a 0, 1, or 2 are listed.

### 9.8.4 The Curly Braces

The curly braces ({}) match for a character or string of characters in a filename.

# EXAMPLE 9.31

```
1 % ls
a.c b.c abc ab3 ab4 ab5 file1 file2 file3 file4 file5 foo faa fumble
2 % ls f{oo,aa,umble}
foo faa fumble
3 % ls a{,.c,c,b}[3-5]
a.c ab3 ab4 ab5
```

# EXPLANATION

- 1 All the files in the current directory are listed.
- 2 Files starting with f and followed by the strings oo, aa, or umble are listed. Spaces inside the curly braces will cause the error message Missing }.
- 3 Files starting with a followed by ., c, c, or b3, b4, or b5 are listed. (The square brackets can be used inside the curly braces.)
