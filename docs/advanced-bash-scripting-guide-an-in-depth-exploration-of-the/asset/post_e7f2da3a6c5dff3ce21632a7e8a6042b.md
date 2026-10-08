
# Chapter 3. Special Characters

What makes a character special? If it has a meaning beyond its literal meaning, a meta-meaning, we refer to it as a special character. Along with commands and keywords, special characters are building blocks of Bash scripts.

## Special Characters Found In Scripts and Elsewhere

- + * Comments. Lines beginning with a # (with the exception of #!) are comments and will not be executed.

```bash
# This line is a comment.
Comments may also occur following the end of a command.
```

```bash
echo "A comment will follow." # Comment here.
# Note whitespace before #
Comments may also follow whitespace at the beginning of the line.
```

```bash
# A tab precedes this comment.
Comments may even be embedded within a pipe.
```

```bash
initial={ cat "startfile" | sed -e '#/d' | tr -d '\n' | \
# Delete lines containing '#' character.
sed -e 's/\_/\_/g' 
# Excerpted from life.sh script
```

> A comment may not follow a comment on the same line. There is no method of terminating the comment, in order for "live code" to begin on the same line. Use a new line for the next command.

> Of, a quoted or an escaped # in an echo statement does not begin a comment. Likewise, it appears in parameter-substitute constructs and in numerical expressions.

```bash
echo "The # here does not begin a comment."
echo 'The # here does not begin a comment.'
echo "The \# here does not begin a comment."
echo "The # here begins a comment."
```

```bash
echo ${PATH}: # Parameter substitution, not a comment.
echo $(( 2#101011 )) # Base conversion, not a comment.
```

## Thanks, S.C.
The standard quoting and escape characters ("\') escape the #.
Pattern matching operations use the #.

Command separator [semicolon]. Permits two or more commands on the same line.

```bash
echo hello; echo there
```

# Advanced Bash-Scripting Guide

```bash
if [ -x "$filename" ]; then
# Note the space after the semicolon.
  echo "File $filename exists."; cp $filename.bak
else
  echo "File $filename not found."; touch $filename
fi
echo "File test complete."
```

Note that the "sometimes needs to be escaped.",

Terminator in a case option [double semicolon].

```bash
case "$variable" in
  abc) echo "\$variable = abc";
  xyz) echo "\$variable = xyz";
  @*)
```

Termin in a case option (version 4+ of Bash).

"dot" command [period]. Equivalent to source (see Example 15-22). This is a bash builtin.

"dot", as a component of filename. When working with filenames, a leading dot is a prefix of the "hidden" file, a file that is not normally show.

```bash
bash$ ls .hidden-file
bash$ ls -l
total 10
-rw-r---- 1 bozo bozo 4034 Jul 18 22:04 datal.addressbook
-rw-r---- 1 bozo bozo 4662 May 25 13:58 datal.addressbook.bak
-rw-r---- 1 bozo bozo 877 Dec 17 2000 employment.addressbook

bash$ ls -al
total 14
drwxrxr-x 2 bozo bozo 1024 Aug 29 20:51 ./
drwx------ 52 bozo bozo 3072 Aug 29 20:51 ../
-rw-r---- 1 bozo bozo 4034 Jul 18 22:04 datal.addressbook
-rw-r---- 1 bozo bozo 4662 May 25 13:58 datal.addressbook.bak
-rw-r---- 1 bozo bozo 877 Dec 17 2000 employment.addressbook
-rw-rw-r 1 bozo bozo 0 Aug 29 20:54 .hidden-file
```

When considering directory names, a single dot represents the current working directory, and two dots de denote the parent directory.

```bash
bash$ pwd
/home/bozo/projects

bash$ cd
bash$ pwd
/home/bozo/projects

bash$ cd
bash$pwd
/home/bozo/bozo/
```

The dot often appears as the destination (directory) of a file movement command, in this context meaning current directory.

# 3. Special Characters

# Advanced Bash-Scripting Guide

```bash
bash$ cp /home/bozo/current_work/junk/*
```

Copy all the "junk" files to $PWD

"dot" character match. When matching characters, as part of a regular expression, a "dot" matches a single character.

partial quoting [double quote]. "STRING" preserves (from interpretation) most of the special characters within STRING. See Chapter 5.

full quoting [single quote]. 'STRING' preserves all special characters within STRING. This is a stronger form of quoting "STRING". See Chapter 5.

comma operator. The comma operator [16] links a series of arithmetic operations. Evaluated, but only the last one is returned.

```bash
let t2 = ((a = 9, 15 / 3))
# Set "a = 9" and "t2 = 15" concatenate strings.
```

```bash
for file in /(usr/bin)/*calc
#   Find all executable files ending in "calc"
#   in /bin and /usr/bin/directories.
do
  if [ -x "$file" ]
    then
      echo $file
  fi

# /bin/ipcalc
# /usr/bin/xcalc
# /usr/bin/oidcalc
# /usr/bin/oocalc
```

Thank you, Rory Winston, for pointing this out.

Lowercase conversion in parameter substitution (added in version 4 of Bash).

escape [backslash]. A quoting mechanism for characters.

\X escapes the character X. This has the effect of "quoting" X, equivalent to 'X'. The \ may be used to quote " ' and '\', so they are expressed literally.

See Chapter 5 for an in-depth explanation of escaped characters.

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename (as in /home/bozo).

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.

Filename path separator [forward slash]. Separates the components of a filename.
