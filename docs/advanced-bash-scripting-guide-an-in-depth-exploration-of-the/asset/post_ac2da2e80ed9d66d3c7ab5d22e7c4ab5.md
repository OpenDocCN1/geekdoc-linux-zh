
# Advanced Bash-Scripting Guide

```
######################################################################
mplayer "$1" -ao pcm:file=$OUTFILE
oggenc "$OUTFILE" # Correct file extension automatically added by oggenc
######################################################################

rm "$OUTFILE"      # Delete intermediate *.wav file.
# If you want to keep it, comment out above line.

exit $?

# Note:
#-
# On a Website, simply clicking on a *.ram streaming audio file
## usually only downloads the URL of the actual *.ra audio file.
# You can then use "wget" or something similar
## to download the *.ra file itself.

#-
# Exercises:
# As is, this script converts *.ra filenames.
## Add flexibility by permitting use of *.ram and other filenames.
#
# If you're really ambitious, expand the script
## to do automatic downloads and conversions of streaming audio files.
# Given a URL, batch download streaming audio files (using "wget")
## and convert them on the fly.
```

A simple example of getopt using substring-extraction constructs.

# Example 10-5. Emulating getopt

```
#!/bin/bash
# getopt-simple.sh
# Author: Chris Morgan
# Used in the ABS Guide with permission.

getopt_simple() {
	echo "getopt_simple()"
	echo "Parameters are '$*'"
	while [ -n "$1" ]
	do
		echo "Processing parameter of: '$1"
		if [ "${1:0:1}" = "-" ]; then
			tmp=${1#*/}      # Strip leading '/' and . .
			parameter=${tmp#*=}      # Extract name.
			value=${tmp#*=}          # Extract value.
			echo "Parameter: '$parameter', value: '$value'"
			eval parameter=$value
		fi
		shift
	done
}
```

Chapter 10. Manipulating Variables

# Advanced Bash-Scripting Guide

```
# Pass all options to getopt_simple().
getopt_simple "$@"
echo test is '$test'
echo test2 is '$test2'
exit 0 # See also, UseGetOpt.sh, a modified version of this script.
```
```

```
sh getopt_example.sh /test=value1 /test2=value2

Parameters are '/test=value1 /test2=value2'
Processing parameter of: '/test=value1'
Parameter: 'test', value: 'value1'
Processing parameter of: '/test2=value2'
Parameter: 'test2', value: 'value2'
test is 'value1'
test2 is 'value2'
```

# Substring Replacement

${string/substring/replacement}
Replace first match of $substring with $replacement.

${string//substring/replacement}
Replace all matches of $substring with $replacement.

```
stringZ=abc123ABCabc      # xyz123ABCabc
echo ${stringZ/abc}       # Replaces first match of 'abc' with 'xyz'.

echo ${stringZ//abc}       # xyz123ABCxyz
# Replaces all matches of 'abc' with 'xyz'.

echo
echo "$stringZ"         # abc123ABCabc
echo                      # The string itself is not altered!

# Can the match and replacement strings be parameterized?
match=abc
repl=000
echo ${string}/$match/${repl} # 000ABC123ABCabc
echo ${string//$match/${repl} # 000ABC123ABC000
# Yes!
echo
# What happens if no replacement string is supplied?
echo ${string/abc}         # 123ABC
echo ${string//abc}        # 123ABC
```

${string/substring/replacement}
If $substring matches front end of $string, substitute $replacement for $substring.
${string%substring/replacement}
If $substring matches back end of $string, substitute $replacement for $substring.

# Chapter 10. Manipulating Variables

# Advanced Bash-Scripting Guide

| stringZ=abcABC123ABCabc | |
|---|---|
| echo ${stringZ#*abc} | # ABC123ABCabc # Replaces front-end match of 'abc' with 'XYZ'. |
| echo ${stringZ%*abc} | # abcABC123ABCabc # Replaces back-end match of 'abc' with 'XYZ'. |

# 10.1.1. Manipulating strings using awk

A Bash script may invoke the string manipulation facilities of awk as an alternative to its built-in operations.

Example 10-6. Alternate ways of extracting and locating substrings

```
#!/bin/bash
# substring-extraction.sh

String=23skidool
# 012345678 Bash
# 123456789 awk
# Note of different string indexing:
# Bash numbers first character of string as 0.
# Awk numbers first character of string as 1.
echo ${String:2:4} # position 3 (0-1-2), 4 characters long
# skid

# The awk equivalent of ${string:pos:length} is substr(string,pos,length)
echo | awk {
  print substr("${String}",3,4) # skid
}

# Piping an empty "echo" to awk gives dummy input,
# that makes it unnecessary to supply a filename.
echo ""

# And like:
echo | awk {
  print substr("${String}",3,"skid") # 3
  # (skid starts at position 3)
}
# The awk equivalent of "index" ...

exit 0
```

# 10.1.2. Further Reference

For more on string manipulation in scripts, refer to Section 10.2 and the relevant section of expr command.

Script examples:

- 1. Example 1-6
- 2. Example 10-9
- 3. Example 10-10
- 4. Example 10-11
- 5. Example 10-13
- 6. Example A-36
- 7. Example A-41

# 10.2. Parameter Substitution

Manipulating and expanding variables

${parameter}
Same as $parameter, i.e., value of variable parameter. In certain contexts, the less ambiguous form works. May be used for concatenating variables with strings.

```bash
your_id=${parameter:-opt/bin}
echo "Old PATH = $PATH"
# Add /opt/bin to PATH for duration of script.
echo "New PATH = $PATH"
```

${parameter:-default}
If not set, use default.

```bash
var=1
var=2
# var3 is unset.
echo ${var1:-var}    # 1
echo ${var3:-2}      # 2
# Note the prefix.
echo ${parameter='whoami'}
# Echoes the result, if variable is still unset.
# Will echo because :- rather than just in condition.
# Compare to first instance, above.

# Once again:
variable=
# variable has been declared, but is set to null.
echo "${variable:-0}" # (no output)
echo "${variable:-1}" # 1
unset variable
echo "${variable:-2}" # 2
echo "${variable:-3}" # 3

exit
```

The default parameter construct finds use in providing "missing" command-line arguments in scripts.

```bash
DEFAULT_FILENAME=generic,data
filename=${1:-DEFAULT_FILENAME}
# If not otherwise specified, the command block operates on the file "generic.data".
# Begin-Command-Block
# #
# End-Command-Block
```

```bash
# From hanoi2.bash example:
DISKS=${1:-E_NOPARAM} # Specify how many disks.
# Set DISKS to $1 command-parameter,
# or to $E_NOPARAM if it is unset.
# See also Example 3-4, and Example A-6.
```

Compare this method using and list to supply a default command-line argument.
${parameter=default}. ${parameter:=default}

If parameter not set, set it to default.

# Advanced Bash-Scripting Guide

Both forms nearly equivalent. The : makes a difference when $parameter has been declared and is null, as above.

```bash
echo $(var=abc)      # abc
echo $(var=xyz)      # abc
# $var already been set to abc, so it did not change.
```

# ${parameter+alt_value}, ${parameter:+alt_value}

If parameter set, use **alt_value**, else use null string.

Both forms nearly equivalent. The : makes a difference when parameter has been declared and is null, see below.

```bash
# $(parameter+alt_value)
a=${param1+xyz}
echo "a = $a"

param2=
a=${param2+xyz}
echo "a = $a"

param3=123
a=${param3+xyz}
echo "a = $a"

# $(parameter:+alt_value)
a=${param4+xyz}
echo "a = $a"

param5=
a=${param5+xyz}
echo "a = $a"
# Different result from a=${param5+xyz}

param6=123
a=${param6+xyz}
echo "a = $a"
```

# ${parameter?err_msg}, ${parameter:+err_msg}

If parameter set, use it, else print err_msg and abort the script with an exit status of 1.

Both forms nearly equivalent. The : makes a difference when parameter has been declared and is null, as above.

Example 10-7. Using parameter substitution and error messages

```bash
#!/bin/bash

# Check some of the system's environmental variables.
# This is good preventative maintenance.
# If, for example, USER, the name of the person at the console, is not set,
# The machine will not recognize you.
```
