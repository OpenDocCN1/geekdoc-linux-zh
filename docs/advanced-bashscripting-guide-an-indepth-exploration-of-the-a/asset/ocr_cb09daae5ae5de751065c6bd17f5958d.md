# Advanced Bash–Scripting Guide

```
echo ${string2%b*c} # abcABC123ABCa
# Strip out shortest between 'b' and 'c', from back of $string

echo ${string%%b*c} # a
# Strip out longest between 'b' and 'c', from back of $string
```

# 9–10. Converting graphic files, with filename change

```
#!/bin/bash
cvt.sh
# Converts all the MacPaint image files in a directory to "pbm" format.

# Uses the "macptopbm" binary from "netpbm" package,
# which is maintained by Brian Henderson (bryanh@giraffe-data.com).
# Netpbm is a standard part of most Linux distros.
```

```
OPERATION=macptopbm
SUFFIX=pbm

# New filename suffix.

if [ -n "$1" ]
then
  directory=$1
  # If directory name given as a script argument
else
  directory=$PWD
  # Otherwise use current working directory.

```

```
# Assumes all files in the target directory are MacPaint image files,
# with a ".mac" suffix.

for file in $directory/*  # Filename globbing.
do
  filename=${file%.*c}
  # Strip ".mac" suffix off filename
  # +('#*.c') matches everything
  # between 'b' and 'c', inclusive).
  $OPERATION file > $filename.$SUFFIX  # Redirect conversion to new filename.
  rm -f "$file"  # Delete original files after converting.
  echo "$filename.$SUFFIX"  # Log what is happening to stdout.
done

exit 0
```

# Substring Replacement

$$(string/substring/replacement)

Replace first match of $substring with $replacement.

$$(string/substring/replacement)

Replace all matches of $substring with $replacement.

```
stringZ=abcABC123ABCabc
echo ${stringZ/abc/xyz}  # xyzABC123ABCabc
# Replaces first match of 'abc' with 'xyz'

echo ${stringZ//abc/xyz}  # xyzABC123ABCxyz
```

# 9.2. Manipulating Strings