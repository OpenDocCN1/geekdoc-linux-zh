# Advanced Bash–Scripting Guide

```
do if [ "$word" > /dev/null
then echo "\$word\ is valid."
else echo "\$word\ is invalid."
fi
done <"$file"
exit 0
```

sed, awk

Scripting languages especially suited for parsing text files and command output. May be embedded singly in combination with pipes and shell scripts.

sed

Non-interactive "stream editor", permits using many ex commands in batch mode. It finds many uses in shell scripts.

awk

Programmable file extractor and formatter, good for manipulating and/or extracting fields (columns) in structured files. Its syntax is similar to C.

wc

wc gives a "word count" on a file or I/O stream:

```
bash$ wc /usr/doc/sed-3.02/README
20 127 838  /usr/doc/sed-3.02/README
[20 lines 127 words 838 characters]
```

wc -w gives only the word count.

wc -l gives only the line count.

wc -c gives only the character count.

wc -L gives only the length of the longest line.

Using wc to count how many .txt files in the current working directory: have a linefeed in their name:

```
$ ls *.txt | wc -l
# Will work as long as none of the "*.txt" files have a linefeed in their name.
# Alternative ways of doing this are:
# find -maxdepth 1 -name \*.txt -print 0 | grep -cz
# (shopt -s nglob); set -- *.txt; echo $$)
```

Thanks, S.C.

Using wc to total up the size of all the files whose begin with letters in the range d–h

```
bash$ wc [d-h]* | grep total | awk '{print $3}'n71832
```

# 12.4. Text Processing Commands

165