
# Advanced Bash-Scripting Guide

```
: ${HOSTNAME} ${USER} ${HOME} ${MAIL}
echo
echo "Name of the machine is $HOSTNAME"
echo "You are $USER"
echo "Your home directory is $HOME"
echo "Your mail INBOX is located in $MAIL"
echo
echo "If you are reading this message,"
echo "critical environmental variables have been set."
echo
echo
```

```
------------------------------------------------------------------------------------------------
The The ${(variablename)} construction can also check
+# for variables within the script.
ThisVariable=Value-of-ThisVariable
+# Note, by the way, that string variables may be set
+# to characters disallowed in their names.
 :# ${ThisVariable}
echo "Value of ThisVariable $ThisVariable"
echo; echo
```

```
: ${(Zxy23AB)?"Zxy23AB has not been set."
# Since Zxy23AB has not been set
+# then the script terminates with an error message.
```

```
# You can specify the error message.
#: ${(variablename)?"ERROR MESSAGE")
```

```
# Same result with:
dummy_variable=$(Zxy23AB)?
dummy_variable=$(Zxy23AB)?"Zxy23AB has not been set."
echo ${(Zxy23AB)? >dev/null
```

```
# Compare these methods of checking a variable has been set
+# with "set-u"
```

```
echo "You will not see this message, because script already terminated.

HERE=0
exit $HERE
# Will NOT exit here.
```

# In fact, this script will return an exit status (echo $?) of 1.

# Example 10-8. Parameter substitution and "usage" messages

```bash
#!/bin/bash
# usage-message.sh
 :# ${1?Usage: 0 ARGUMENT}
# Script exits here if command-line parameter absent,
+# with following error message.
# usage-message.sh 1: Usage-usage-message.sh ARGUMENT
```

# Chapter 10. Manipulating Variables

# Advanced Bash-Scripting Guide

echo "These two lines echo only if command-line parameter given.
echo "command-line parameter = \$1"

exit 0 # Will exit here only if command-line parameter present.

# Check the exit status, both with and without command-line parameter.
# If command-line parameter present, then "$#" is 0.
# If not, then "$?" is 1.

Parameter substitution and/or expansion. The following expressions are the complement to the match in string operations (see Example 16-9). These particular ones are mostly used in parsing file names.

# Variable length / Substring removal

$#var

String length (number of characters in $var). For an array, $(#array) is the length of the first element in the array.

- Exceptions:
    * ${#*} and ${#@} give the number of positional parameters.
    * For an array, ${#array[*]} and ${#array[@]} give the number of elements in the array.

# Example 10-9. Length of a variable

```bash
#!/bin/bash
# length.sh

E_NO_ARGS=65

if [ $# -eq 0 ]; # Must have command-line args to demo script.
then
echo "Please invoke this script with one or more command-line arguments."
exit $E_NO_ARGS
fi

var01=abcdEFGH28ij
echo var01=${#var01}
echo "Length of var01 = ${#var01}"
# Now, let's try embedding a space.
var02="abcd EFGH28ij"
echo var02=${#var02}
echo "Length of var02 = ${#var02}"

echo "Number of command-line arguments passed to script = ${#}"
echo "Number of command-line arguments passed to script = ${#*}\"

exit 0
```

${var#Pattern}, ${var##Pattern}

${var#Pattern} Remove from $var the shortest part of $Pattern that matches the front end of $var.

$${var##Pattern} Remove from $var the longest part of $Pattern that matches the front end of $var.

A usage illustration from Example A-7:

```bash
# Function from "days-between.sh" example.
# Strips zero(s) from argument passed.
strip_leading_zero () # Strip possible leading zero(s)
{
# from argument passed.
  # The "1" refers to "$1" passed arg.
  return=${1#0}
} # The "0" is what to remove from "$1" strips zeros.
```

Manfred's elaborate elaborate of the above:

```bash
strip_leading_zero2 () # Strip possible leading zero(s), since otherwise
{
 Bash will interpret such numbers as octal values.
  shopt -u extglob; # Turn off extended globbing.
  local val=${1#+#} # Use local variable, longest matching series of 0's.
  shopt -u extglob; # Turn off extended globbing.
  _strip_leading_zero2=${val:0,0} # If input was 0, return 0 instead of ""
}
```

Another usage illustration:

```bash
echo basename $PWD # Name of current directory.
echo "${PWD##*/}" # Name of directory.
echo basename $0 # Name of script.
echo $0 # Name of script.
echo "${0##*/}" # Name of script.
echo filename=test.data # data
echo "${filename##*.}" # Extension of filename.
```

# ${var#Pattern}, ${var##Pattern}

${var%Pattern} Remove from $var the shortest part of $Pattern that matches the back end of $var.

${var%%Pattern} Remove from $var the longest part of $Pattern that matches the back end of $var.

Version 2 of Bash added options.

# Example 10-10. Pattern matching in parameter substitution

```bash
#!/bin/bash
# patt-matching.sh
# Pattern matching using # % parameter operators.
var=abcd12345
pattern1=*c (wild card) matches everything between a - c.
```

# Chapter 10. Manipulating Variables

```bash
echo $var # abcd12345
echo $var = $(var) # abcd12345
(alternate form)
echo "Number of characters in ${var} = ${#var}"
```

```bash
echo "pattern1 = $pattern1 # a*c (everything between 'a' and 'c')
echo
echo '${var#$pattern1}' = '${var#$pattern1}' # d12345
# Shortest possible match, strips out 3 characters abcd12345
echo '${var###pattern1}' = '${var###pattern1}' # 6789
# Longest possible match, strips out 12 characters abcd12345
echo
```

```bash
pattern2=b* # everything between 'b' and '9'
echo var = $var # Still abcd12345
echo "pattern2 = $pattern2"
echo
echo '${var%%$pattern2}' = '${var%%$pattern2}' # abcd12345
# Shortest possible match, strips out last 6 characters abcd12345
echo '${var%%*pattern2}' = '${var%%*pattern2}' # a
# Longest possible match, strips out last 12 characters abcd12345
```

Remember, # and ## work from the left end (beginning) of string,
% and %% work from the right end.
echo
echo 0
```

# Example 10. Renaming files:

```bash
#!/bin/bash
# rfe.sh: Renaming file extensions.
rfe old_extension new_extension
# Example:
# To rename all *.files in working directory to *.jpg,
rfe gif jpg
```

```bash
E_BADARGS=$# # The vertical bars mean "or" in this context.
case $E_BADARGS in
0|1)
echo "Usage: $0 old_file_suffix new_file_suffix"
exit $_BADARGS # If 0 or 1 arg, then bail out.
;;
esac

for filename in *. # Traverse list of files ending with 1st argument.
do
mv $filename ${filename%$1}$2
# Strip off part of filename matching 1st argument
+# then append 2nd argument.
done
exit 0
```

# Variable expansion /Substring replacement

These constructs have been adopted from ksh.

# ${var:pos}

Variable var expanded, starting from offset pos.

# ${var:len}

Expansion to a max len characters of var, from offset pos. See Example A-13 for an example of the creative use of this operator.

# ${var/Pattern/Replacement}

First match of Pattern, within var replaced with Replacement.

If Replacement is omitted, the first match of Pattern is replaced by nothing, that is, deleted.

# ${var/Pattern/Replacement}

Global replacement. All matches of Pattern, within var replaced with Replacement.

As above, if Replacement is omitted, then all occurrences of Pattern are replaced by nothing, that is, deleted.

# Example 10-12. Using pattern to parse arbitrary strings

```bash
#!/bin/bash
var=abcd-1234-defg
echo var = $var

t=${var#*-}
echo "$t (with everything, up to including first stripped out) = $t"
# ${var#*-} works the shortest string,
+# since * matches everything preceding, including an empty string.
# (Thanks, Stephane Chazelas, for pointing this out.)

t=${var%%-*}
echo "$t contains a -*", returns empty string... 
var = $t

t=${var#*-}
echo "$t (with everything from the last - on stripped out) = $t"

path_name=/home/bozo/thoughts.for.today
echo "$path_name#*/"
t=${path_name#*/}
echo "$path_name, stripped of prefixes = $t"
# Same effect as t='$path_name' in this particular case.
```
