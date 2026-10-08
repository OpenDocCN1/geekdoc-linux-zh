You can split a line by substituting a newline character into it. The application must escape the newline character in replacement by preceding it with a backslash. A substitution is considered to have been performed even if the replacement string is identical to the string that it replaces. For a fuller description see sed(1); flags is zero or more of the following:

+   - n=1 - 512. Substitute for just the n-th occurrence of the regular expression

+   - g Globally substitute all nonoverlapping instances of the regular expression instead of the first one. If you use both g and n, the results are unspecified

+   - p Print the pattern space if a replacement was made.

+   - p Print the initial segment of the pattern space through the first newline to the standard output

+   - wfile Write by appending the pattern space to wfile if a replacement was made. The first occurrence of w clears wfile. Subsequent invocations of w append to wfile. Each time you use the sed command, wfile is overwritten.

+   - y/string1/string2/

Replace all occurrences of characters in string1 with the corresponding characters in string2; string1 and string2 must have the same number of characters; otherwise, if any of the characters in string1 are undefined. You can use any character other than backslash and newline instead of slash to delimit the strings. Within string1 and string2, you can use the delimiter itself as a literal character if it is preceded with a backslash. For example, y/abc/ABC replaces a with A, b with B, and c with C.

See largefile(5) for the description of the behavior of sed when encountering files greater than or equal to 2 Gbytes (2**31 bytes).

# Examples

The following sed script simulates the BSD cat -s command by squeezing excess blank lines from standard input:

```
sed -n '
# Write nonempty lines.
./
p
d
}
# Write a single empty line, then look for more empty lines.
^S/
p# Get next line, discard the held newline (empty line),
```