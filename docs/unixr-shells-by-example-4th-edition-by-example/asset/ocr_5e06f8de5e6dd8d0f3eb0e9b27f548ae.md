# EXAMPLE 4.2

```
ps -ef | grep root
```

# EXPLANATION

The output of the ps command (ps -ef displays all processes running on this system) is sent to grep and all lines containing root are printed.

# 4.1.3 Metacharacters

A metacharacter is a character that represents something other than itself. ^ and $ are examples of metacharacters.

The grep command supports a number of regular expression metacharacters (see Table 4.1) to help further define the search pattern. It also provides a number of options (see Table 4.2) to modify the way it does its search or displays lines. For example, you can provide options to turn off case sensitivity, display line numbers, display errors only, and so on.

# EXAMPLE 4.3

```
grep -n '^jack:' /etc/passwd
```

# EXPLANATION

Grep searches the /etc/passwd file for jack; if jack is at the beginning of a line, grep prints out the number of the line on which jack was found and where in the line jack was found.

# Table 4.1 grep's Regular Expression Metacharacters

| Metacharacter | Function | Example | What It Matches |
| ^ | Beginning-of-line anchor | '^love' | Matches all lines beginning with love. |
| $ | End-of-line anchor | 'love$' | Matches all lines ending with love. |
| . | Matches one character | '1..e' | Matches lines containing an 1, followed by two characters, followed by an e. |
| * | Matches zero or more characters preceding the asterisk | '*love' | Matches lines with zero or more spaces, followed by the pattern love. |
| [ ] | Matches one character in the set | '[Ll]ove' | Matches lines containing love or Love. |