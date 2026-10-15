The output of the print function can be redirected or piped to another program, and the output of another program can be piped to awk for printing. (See "Redirection" on page 25 and "Pipes" on page 28.)

# EXAMPLE 6.5

```
% date
Wed Jul 28 22:23:16 PDT 2004

% date | awk '{ print "Month: " $2 "\nYear: " , $6 }'
Month: Jul
Year: 2004
```

# EXPLANATION

The output of the UNIX date command will be piped to awk. The string Month: is printed, followed by the second field, the string containing the newline character (\n), and Year:, followed by the sixth field ($6).

# Escape Sequences.

Escape sequences are represented by a backslash and a letter or number. They can be used in strings to represent tabs, newlines, form feeds, and so forth (see Table 6.1).

# Table 6.1 print Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| \b | Backspace |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Tab |
| \047 | Octal value 47, a single quote |
| \c | c represents any other character, e.g., \ |

# EXAMPLE 6.6

Tom Jones 4424 5/12/66 543254
Mary Adams 5346 11/4/63 28765
Sally Chang 1654 7/22/34 650000
Billy Black 1683 9/23/44 336500

```
% awk '/Sally/{print "\t\tHave a nice day, "$1, $2 "\"!"}' employees
Have a nice day, Sally Chang!
```