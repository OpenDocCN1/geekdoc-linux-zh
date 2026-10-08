
# Advanced Bash-Scripting Guide

```
# No parameter substitution when the "limit string" is quoted or escaped.
# Either of the following at the head of the here document would have
# the same effect.
# cat <<"Endofmessage"
# cat <<\Endofmessage
```

```bash
# And, likewise:
cat <<"SpecialChartTest"
Directory listing would follow
if limit string were not quoted.
ls -1
Arithmetic expansion would take place
if limit string were not quoted.
A single backslash would echo
if limit string were not quoted.
\\\
SpecialChartTest
exit
```

Disabling parameter substitution permits outputting literal text. Generating scripts or even program code is one use for this.

# Example 19-8. A script that generates another script

```bash
#!/bin/bash
# generate-script.sh
# Based on an idea by Albert Reiner

OUTFILE=generated.sh      # Name of the file to generate.

----------------------------------------------------------------------
# 'Here document containing the body of the generated script.
cat <<'EOF'
#/bin/bash
```

```bash
echo "This is a generated script."
# Note that we are inside a subshell,
# we can't access variables in the "outside" script.

echo "Generated file will be named: $OUTFILE"
# Above line will not work as normally expected
# because parameter expansion has been disabled.
# Instead, the result is literal output.
```

# Chapter 19. Here Documents

# Advanced Bash-Scripting Guide

```bash
a=7
b=3

let "c = $a * $b"
echo "c = $c"

exit 0
EOF
) > $OUTFILE
# ---
```

# Quoting the 'limit string' prevents variable expansion
## within the body of the above 'here document.'
# This permits outputting literal strings in the output file.

```bash
if [ -f "OUTFILE" ]
then
  chmod 755 $OUTFILE
  # Make the generated file executable.
else
  echo "Problem in creating file: $OUTFILE"
fi
```

# This method also works for generating
## C programs, Perl programs, Python programs, Makefiles,
## and the like.

```bash
exit 0
```

It is possible to set a variable from the output of a here document. This is actually a devious form of command substitution.

```bash
variable=$$(cat <<SETVAR
This variable
runs over multiple lines.
SETVAR
)
```

```bash
echo "$variable"
```

A here document can supply input to a function in the same script.

Example 19-9. Here documents and functions

```bash
#!/bin/bash
# here-function.sh

GetPersonalData ()
{
  read firstname
  read lastname
  read address
  read city
  read state
  read zipcode
)# This certainly appears to be an interactive function, but . . .
```

Chapter 19. Here Documents

# Advanced Bash-Scripting Guide

```bash
# Supply input to the above function.
GetPersonalData <<RECORD001
Bozo
Bozeman
2726 Nondescript Dr.
Bozeman
MT
21226
RECORD001

echo "$firstname $lastname"
echo "$address"
echo "$city, $state $zipcode"
echo

exit 0
```

It is possible to use : as a dummy comment accepting output from here a document. This is, in effect, creates "anonymous" here document.

# Example 19-10. "Anonymous" Here Document

```bash
#!/bin/bash
: <<TESTVARIABLES
${HOSTNAME}?${USER}?${MAIL?}\  # Print error message if one of the variables not set.
TESTVARIABLES

exit $?
```

> A variation of the above technique "commenting out" blocks of code.

# Example 19-11. Commenting out block of code

```bash
#!/bin/bash
# commentblock
: <<COMMENTBLOCK
echo "This line will not echo."
This is a comment line missing the "#" prefix.
This is another comment line missing the "#" prefix.

*&!+++
The above line will cause no error message,
because the Bash interpreter will ignore it.
COMMENTBLOCK

echo "Exit value of \$COMMENTBLOCK" is $?.  # 0
# No error shown.
echo
```

# The above technique also comes useful for commenting out
# block of working for debugging purposes.
# This saves having to put a "#" at the beginning of each line,

# Chapter 19. Here Documents

```bash
# then having to go back and delete each "# later.
# Note that the use of colon, above, is optional.

echo "Just before commented-out code block."
# The lines of code between the double-dashed lines will not execute.
######################################################################
: <<DEBUGUGXX
for file in *
do
cat "$file"
done
DEBUGUGXX
######################################################################
echo "Just after commented-out code block."

exit 0
```

```bash
# Note, however, if a bracketed variable is contained within
# the commented-out code block,
# then this could cause problems.
# for example:

#!/bin/bash

# <<COMMENTBLOCK
echo "This line will not echo."
$!
$(foo_bar_bazz)
$(rm -rf /tmp/foobar/)
$(touch my_build_directory/cups/Makefile)
COMMENTBLOCK
```

$ sh commented-bad.sh
commented-bad.sh: line 3: foo_bar_bazz: parameter null or not set

# The remedy for this is to strong-quote the 'COMMENTBLOCK' in line 49, above.
# <<'COMMENTBLOCK'

Yet another twist of this nifty makes "self-documenting" scripts possible.

# Example 19-12. A self-documenting script

```bash
#!/bin/bash
# self-documenting.sh: self-documenting script
# Modification of "colm.sh"

DOC_REQUEST=70

if [ "$1" = "-h" -o "$1" = "--help" ]; then Request help.
then
echo " " Usage: $0 [directory-name] "; echo
sed --silent -e '/DOCUMENTATION$$/,/DOCUMENTATION$$/p' "$0" |
```

# Chapter 19. Here Documents

# Advanced Bash-Scripting Guide

```bash
sed -e '/DOCUMENTATIONXX$/d'; exit $DOC_REQUEST; fi

: <<DOCUMENTATIONXX
List the statistics of a specified directory in tabular format.

The command-line parameter gives the directory to be listed.
If no directory specified or directory specified cannot be read,
then list the current working directory.

```bash
DOCUMENTATIONXX

if [ -z "$1" -o -r "$1" ]
then
directory=
else
directory="$1"
fi
```

```bash
echo "Listing of "$directory":"; echo
printf "PERMISSIONS LINKS OWNER GROUP SIZE MONTH DAY HH:MM PROG-NAME\n" \n; ls -l "$directory" | sed 1 | column -t
```

exit 0
Using a cat script is an alternate way of accomplishing this.

```bash
DOC_REQUEST=70
if [ "$1" = "-h" -o "$1" = "--help" ] # Request help.
Use a "cat script"
then
cat <<DOCUMENTATIONXX
List the statistics of a specified directory in tabular format.
```

The command-line parameter gives the directory to be listed.
If no directory specified or directory specified cannot be read,
then list the current working directory.

```bash
DOCUMENTATIONXX
exit $DOC_REQUEST
fi
```

See A-28, A-40, A-41, A-42 for more examples of self-documenting scripts.

> Here create temporary files, but these files are deleted after opening and are not accessible to any other process.

```
bash -c 'lsof -a p -sd0' EOF
> EOF
lsof 1 REG 03386 /tmp/t1213 (deleted)
```

+   Some utilities will not work inside a here document.

+   The closing limit string, on the final line of a here document, must start in the first character position. There can be leading whitespace. Trailing whitespace after the limit string causes unexpected behavior. The whitespace prevents the limit string from being recognized.

# Advanced Bash-Scripting Guide

```bash
#!/bin/bash
echo "-LimitString
cat <<-echo "This is line 1 of the message inside the here document."
echo "This is line 2 of the message inside the here document."
echo "This is the final line of the message inside the here document."
LimitString
Indented limit string. Error! This script will not behave as expected."
echo "
```

# These comments are outside the 'here document'
## and should not echo.

echo "Outside the here document."
exit 0
echo "This line had better not echo." # Follows an 'exit' command.

Some people cleverly use a 'single' as a limit string. But that's not necessarily a good idea.

```bash
# This works.
cat <<!
Hello!
! Three more exclamations !!!
!
# But . . .
cat <<!
Hello!
Single exclamation point follows!
!
# Crashes with an error message.

# However, the following will work.
cat <<EOF
Hello!
Single exclamation point follows!
!
EOF
# It's safer to use a multi-character limit string.
```

For those tasks too complex for a here document, consider using the expect scripting language, which specifically designed for feeding input into interactive programs.

# 19.1. Here Strings

A here
string can be considered as a stripped-down form of a here document.
