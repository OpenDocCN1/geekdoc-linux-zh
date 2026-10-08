and IFS, HOME, SHELL, ENV, and MAIL are never set automatically by the shell (although HOME, SHELL, and MAIL are set by login(l)).

# Blank Interpretation

After parameter and command substitution, the results of substitution are scanned for field separator characters (found in IFS), and split into distinct arguments where such characters are found. ksh retains explicit null arguments ( or ') but removes implicit null arguments (those resulting from parameters that have no values).

# File Name Generation

Following substitution, each command word is processed as a pattern for file name expansion unless the -f option has been set. The form of the patterns is the Pattern Matching Notation defined by regexp(5). The word is replaced with sorted file names matching the pattern. If no file name is found that matches the pattern, the word is left unchanged.

In addition to the notation described in regexp(5), ksh recognizes composite patterns made up of one or more pattern lists separated from each other with a |. Composite patterns can be formed with one or more of the following:

+   *   ?(pattern-list) - Optionally matches any one of the given patterns.
*   \*(pattern-list) - Matches zero or more occurrences of the given patterns.
*   +(pattern-list) - Matches one or more occurrences of the given patterns.
*   @(pattern-list) - Matches exactly one of the given patterns.
*   !(pattern-list) - Matches anything, except one of the given patterns.

# Quoting

Each of the metacharacters listed above (See Definitions above) has a special meaning to the shell and causes termination of a word unless quoted. A character can be quoted (i.e., made to stand for itself) by preceding it with a \ . The pair \ newline is ignored. All characters enclosed between a pair of single quote marks ('), are quoted. A single quote cannot appear within single quotes. Inside double quote marks ("), parameter and command substitution occurs and \ quotes the characters \, ', ", and $. $ and $\ have identical meanings when not quoted or when used as a parameter assignment value or as a file name. However, when used as a command argument, "*\$*" is equivalent to "\$1\$2\$2...", where d is the first character of the IFS parameter, whereas "\$\$" is equivalent to "\$1" "\$2" .... Inside back single quote (accent grave) marks (`) \ quotes the characters \, ', and $. If the back single quotes occur within double quotes, \ also quotes the character ".

The special meaning of keywords or aliases can be removed by quoting any character of the keyword. The recognition of function names or special command names listed below cannot be altered by quoting them.

# Arithmetic Evaluation

The ability to perform integer arithmetic is provided with the special command let. Evaluations are performed using long arithmetic. Constants take the form [base#]n, where base is a decimal number between two and thirty-six representing the arithmetic base and n is a number in that base. If base is omitted, base 10 is used.

An arithmetic expression uses the same syntax, precedence, and