# Table 6.12 Built-In Variables (continued)

| Variable Name | Contents |
|---|---|
| RSTART | Offset of string matched by match function |
| RT | The record terminator; gawk sets it to the input text that matched the character or regex specified by RS |
| SUBSEP | Subscript separator |

# EXAMPLE 6.90

(The Employees Database)
% cat employees2
Tom Jones:4423:5/12/66:543354
Mary Adams:5346:11/4/63:28765
Sally Chang:1654:7/22/54:650000
Mary Black:1683:9/23/44:336500

(The Command Line)
% nawk -F: '$1 == "Mary Adams"{print NR, $1, $2, $NF}' employees2

(The Output)
2 Mary Adams 5346 28765

# EXPLANATION

The -F option sets the field separator to a colon. The print function prints the record number, the first field, the second field, and the last field ($NF).

# EXAMPLE 6.91

(The Employees Database)
% cat employees2
Tom Jones:4423:5/12/66:543354
Mary Adams:5346:11/4/63:28765
Sally Chang:1654:7/22/54:650000
Mary Black:1683:9/23/44:336500

(The Command Line)
% gawk -F: '{IGNORECASE=1; $1 == "mary adams"{print NR, $1, $2,$NF}' employees2

(The Output)
2 Mary Adams 5346 28765