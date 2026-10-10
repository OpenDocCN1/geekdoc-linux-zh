Perfect! The commands scanned the file and found three repeating lines. Now we can prettify this up, and store it in a shell wrapper. Here’s one way to do it:

```
```
$ cat NeededFunctionCheck.sh
#!/bin/bash
# Checks for 3 duplicate lines in scripts.
# Suggest these lines be possibly replaced
# by a function.
#
tempfile=$2
#
#
sed -n '{
1N; N;
s/ /g; s\t//g;
s\n/a/g; p;
s/\\a\n/; D]' $1>> $tempfile
# sort $tempfile | uniq -d | sed 's/a/\n/g'
# rm -i $tempfile

exit
$  
```
```

Notice that this script takes two parameters — the first ($1) for which file to scan, and the second ($2) to designate a temporary file to store the merged file lines. The reason we redirected STDOUT to a file, instead of directly into the sort command, is that it gives you the ability to keep the temporary file to see if your sed merging process (and any tweaks you make to it) are working correctly.

Before you start diving into modifying this script to try out variations, let’s scan our test text file with it:

```
```
$ ./NeededFunctionCheck.sh ScriptDataB.txt TempFile.txt
Line3
Line4
Line5
rm: remove regular file 'TempFile.txt'? Y
$  
```
```

This is exactly what we are wanting. Now, let’s try scanning a real script and see how it does: