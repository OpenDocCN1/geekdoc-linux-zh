
# Advanced Bash–Scripting Guide

```
echo
echo 'IFS unchanged, using "$*"'
c=0
for i in "$*"    # quoted
doo echo "$((c+1)): [$i]" # This line remains the same in every instance.
                                     # Echo args.
done
d
echo ---
echo 'IFS unchanged, using $*'
c=0
for i in $*       # unquoted
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS unchanged, using "$@"'
c=0
for i in "$@"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS unchanged, using $0'
c=0
for i in "$0"
doo echo "$((c+1)): [$i]"
done
echo ---
IFS=
echo 'IFS=":", using "$*"'
c=0
for i in "$*"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS=":", using $*'
c=0
for i in *
doo echo "$((c+1)): [$i]"
done
echo ---
var=$* 
echo 'IFS=":", using "$var" (var=$*)'
c=0
for i in "$var"
doo echo "$((c+1)): [$i]"
done
echo ---
echo 'IFS=":", using $var (var=$*)'
c=0
for i in $var
doo echo "$((c+1)): [$i]"
done
echo ---
```

## Chapter 9. Variables Revisited

```
var="$*"
echo IFS=":", using var(var="$*")
c=0
for i in $var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="$*")
c=0
for i in "\$var"
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$\$@"
c=0
for i in "\$@"
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$@'
c=0
for i in \$@$
doo echo "$((c+=1)): [$i]"
done
echo ---
var="\$@"
echo IFS=":", using var(var="\$@")
c=0
for i in $var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="\$@")
c=0
for i in \$var
doo echo "$((c+=1)): [$i]"
done
echo ---
echo IFS=":", using \$var(var="\$@")
c=0
for i in \$var
doo echo "$((c+=1)): [$i]"
done
echo ---
# Try this script with ksh or zsh -y.
```

# Advanced Bash–Scripting Guide

exit 0

The $$ and \$ parameters differ only when
between double quotes.

# Example 9–8. $* and @@ when $IFS is empty

```bash
#!/bin/bash

# If IFS set, but empty,
then "$*" and "@@" do not echo positional params as expected.

# Echo positional parameters.
mecho () {
  echo "$1,$2,$3"
}

IFS="" # Set, but empty.
set a b c  # Positional parameters.

mecho "$*" # abc,
mecho $* # a,bc
mecho @@ # a,b,c
mecho "@@" # a,b,c

# The behavior of $* and @@ when $IFS is empty
# on whatever Bash or sh version being run.
# It is therefore inadmissible to depend on this "feature" in a script.

# Thanks, S.C.
exit 0
```

# Special Parameters

- $-`: Flags passed to script. This was originally a ksh construct adopted into
Bash, and unfortunately it does not seem to work
reliably in Bash scripts. One possible use for it
to have a script self-test whether it is interactive.

- `$!`: PID (process id) of last job run in background

- `$_`: Special variable set to last argument of previous command executed.

## Chapter 9. Variables Revisited

# Advanced Bash–Scripting Guide

Example 9–9. underscore variable

```bash
#!/bin/bash
echo $_          # Just called /bin/bash to run the script.
du >/dev/null      # So no output from command.
ls -al             # So no output from command.
echo $_           #: status of a command, function, or the script itself (see Example 23–24, and 12–23)
```

## 9.2. Manipulating Strings

- `${string}`: Length
```bash
string=abc123ABCc
echo ${#string}      # 11
```

- `${string:length}`: Length of Substring at Beginning of String
```bash
string=abc123ABCc
echo ${string:0}      # 11
```

- `${string#pattern}`: Length of Matching Substring at Beginning of String ($substring is a regular expression).
```bash
string=abc123ABCc
echo ${string#abc}  # 8
```

- `${string%%pattern}`: Index (Numerical position of first character in substring that matches).
```bash
string=abc123ABCc
echo ${string%%ABC*}  # 6
```

- `${string##pattern}`: Index (Numerical position before '1').
```bash
string=abc123ABCc
echo ${string##abc*}  # 3
```

- `${string:position}`: Substring Extraction (If the string parameter is "*" or "@", then it extracts positional parameters starting at position).
```bash
string=abc123ABCc
echo ${string:7}      # 23ABC (Wait, the OCR text says 23ABC logic)
```

- `${string:position:length}`: Substring Extraction (If the string parameter is "*" or "@", then it extracts a maximum of length parameters, starting at position).
```bash
string=abc123ABCc
echo ${string:2:3}    # bc
```

- `${string%pattern}`: Substring Removal (Strips shortest match between 'b' and 'c', from back of $string).
```bash
string=abc123ABCc
echo ${string%b*c}    # abc123ABCa
```

- `${string%%pattern}`: Substring Removal (Strips longest match between 'b' and 'c', from back of $string).
```bash
string=abc123ABCc
echo ${string%%b*c}    # a
```

- `${string#pattern}`: Substring Removal (Strips shortest match between 'a' and 'C').
```bash
string=abc123ABCc
echo ${string#*aC}    # 123
```

- `${string##pattern}`: Substring Removal (Strips longest match between 'a' and 'C').
```bash
string=abc123ABCc
echo ${string##*a*}   # abc
```

- `${string##pattern}`: Substring Removal (Strips longest match of $substring from back of $string).
- `${string%%pattern}`: Substring Removal (Strips longest match of $substring from back of $string).

## 9–10. Converting graphic files, with filename change

```bash
#!/bin/bash
cvt.sh
# Converts all the MacPaint image files in a directory to "pbm" format.

# Uses the "macptopbm" binary from "netpbm" package,
# which is maintained by Brian Henderson (bryanh@giraffe-data.com).
# Netpbm is a standard part of most Linux distros.
```

```bash
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

## Assumes all files in the target directory are MacPaint image files,
# with a ".mac" suffix.

for file in $directory/*  # Filename globbing.
do
  filename=${file%.*c}
  # Strip ".mac" suffix off filename
  $OPERATION file > $filename.$SUFFIX  # Redirect conversion to new filename.
  rm -f "$file"  # Delete original files after converting.
  echo "$filename.$SUFFIX"  # Log what is happening to stdout.
done

exit 0
```
