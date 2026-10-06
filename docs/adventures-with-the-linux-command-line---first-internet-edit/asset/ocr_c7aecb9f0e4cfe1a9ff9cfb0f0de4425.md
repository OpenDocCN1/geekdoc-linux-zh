```
)} # Closing brace for action
```

# Patterns

Here are the most common types of patterns used in AWK:

# BEGIN and END

As we saw earlier, the BEGIN and END patterns perform actions before the first record we read and after the last record is read, respectively.

# relational-expression

Relational expressions are used to test values. For example, we can test for equivalence

```
$1 == "Fedora"
```

or for relations such as:

```
$3 >= 50
```

It is also possible to perform calculations like:

```
$1 * $2 < 100
```

# /regular-expression/

AWK supports regular expressions like those supported by egrep. Patterns using regular expression can be expressed in two ways. First, we can choose a regular expression in slashes and a match is attempted on the entire record. If a finer level of control is needed, we can provide an expression containing the string to be matched using the following syntax:

```
expression ~ /regexp/
```

For example, if we only wanted to attempt a match on the third field in a record, we could do this:

```
$3 ~ /^[567]/
```

From this, we can think of the "~" as meaning "matches" or "contains", thus we can read the pattern as "field 3 matches the regular expression ^[567]".

# pattern logical-operator pattern

It is possible to combine patterns together using the logical operators || and &&, meaning OR and AND. For example, if we want to test a record to see if the first field is a number greater than 100 and the last field is the word "Debit", we can do this:

```
$1 > 100 && $NF == "Debit"
```

AWK 95