
Which PID has higher priority?

PID 12.

4. After trying to renice a process with renice, the following error happens:

```
$ renice -10 21704
renice: failed to set priority for 21704 (process ID): Permission denied
```

What is the probable cause for the error?

Only user root can decrease nice numbers below zero.

## Answers to Explorational Exercises

1. Changing process priorities is usually required when a process is occupying too much CPU time. Using ps with standard options for printing all system processes in long format, what --sort flag will sort processes by CPU utilization, increasing order?

```
$ ps -e1 --sort=pcpu
```

2. Command schedtool can set all CPU scheduling parameters Linux is capable of or display information for given processes. How can it be used to display the scheduling parameters of process 1750? Also, how can schedtool be used to change process 1750 to real-time with priority -90 (as displayed by top)?

```
$ schedtool 1750
```

```
$ schedtool -R -p 89 1750
```

![image](img/824749d5fc1d265354d0e66a01af9ced_369_0.png)

## 103.7 Search text files using regular expressions

### Reference to LPI objectives

LPI-1 v5, Exam 101, Objective 103.7

### Weight

3

### Key knowledge areas

- Create simple regular expressions containing several notational elements.
- Understand the differences between basic and extended regular expressions.
- Understand the concepts of special characters, character classes, quantifiers and anchors.
- Use regular expression tools to perform searches through a filesystem or file content.
- Use regular expressions to delete, change and substitute text.

### Partial list of the used files, terms and utilities

- **grep**
- **egrep**
- **fgrep**
- **sed**
- **regex (7)**

![image](img/824749d5fc1d265354d0e66a01af9ced_370_0.png)

## 103.7 Lesson 1

| Certificate: | LPIC-1 |
| :--- | :--- |
| Version: | 5.0 |
| Topic: | 103 GNU and Unix Commands |
| Objective: | 103.7 Search text files using regular expressions |
| Lesson: | 1 of 2 |

### Introduction

String-searching algorithms are widely used by several data-processing tasks, so much that Unix-like operating systems have their own ubiquitous implementation: *Regular expressions*, often abbreviated to *REs*. Regular expressions consist of character sequences that make up a generic pattern used to locate and sometimes modify a corresponding sequence in a larger string of characters. Regular expressions greatly expand the ability to:

-   *Write parsing rules to requests in HTTP servers, nginx in particular.*
-   *Write scripts that convert text-based datasets to another format.*
-   *Search for occurrences of interest in journal entries or documents.*
-   *Filter markup documents, keeping semantic content.*

The simplest regular expression contains at least one *atom*. An atom, so named because it's the basic element of a regular expression, is just a character that may or may not have special meaning. Most ordinary characters are unambiguous, they retain their literal meaning, while others have special meaning:

-   **. (dot)**
    Atom matches with any character.
-   **^ (caret)**
    Atom matches with the beginning of a line.
-   **$ (dollar sign)**
    Atom matches with the end of a line.

For example, the regular expression bc, composed by the literal atoms b and c, can be found in the string abcd, but can not be found in the string a1cd. On the other hand, the regular expression .c can be found in both strings abcd and a1cd, as the dot . matches with any character.

The caret and dollar sign atoms are used when only matches at the beginning or at the end of the string are of interest. For that reason they are also called anchors. For example, cd can be found in abcd, but ^cd can not. Similarly, ab can be found in abcd, but ab$ can not. The caret ^ is a literal character except when at the beginning and $ is a literal character except when at the end of the regular expression.

### Bracket Expression

There is another type of atom named *bracket expression*. Although not a single character, brackets [] (including their content) are considered a single atom. A bracket expression usually is just a list of literal characters enclosed by [], making the atom match any single character from the list. For example, the expression [1b] can be found in both strings abcd and a1cd. To specify characters the atom should not correspond to, the list must begin with ^, as in [^1b]. It is also possible to specify ranges of characters in bracket expressions. For example, [0-9] matches digits 0 to 9 and [a-z] matches any lowercase letter. Ranges must be used with caution, as they might not be consistent across distinct locales.

Bracket expression lists also accept classes instead of just single characters and ranges. Traditional character classes are:

-   **[:alnum:]**
    Represents an alphanumeric character.
-   **[:alpha:]**
    Represents an alphabetic character.
-   **[:ascii:]**
    Represents a character that fits into the ASCII character set.
-   **[:blank:]**
    Represents a blank character, that is, a space or a tab.
-   **[:cntrl:]**
    Represents a control character.
-   **[:digit:]**
    Represents a digit (0 through 9).
-   **[:graph:]**
    Represents any printable character except space.
-   **[:lower:]**
    Represents a lowercase character.
-   **[:print:]**
    Represents any printable character including space.
-   **[:punct:]**
    Represents any printable character which is not a space or an alphanumeric character.
-   **[:space:]**
    Represents white-space characters: space, form-feed (\f), newline (\n), carriage return (\r), horizontal tab (\t), and vertical tab (\v).
-   **[:upper:]**
    Represents an uppercase letter.
-   **[:xdigit:]**
    Represents hexadecimal digits (0 through F).

Character classes can be combined with single characters and ranges, but may not be used as an endpoint of a range. Also, character classes may be used only in bracket expressions, not as an independent atom outside the brackets.

### Quantifiers

The reach of an atom, either a single character atom or a bracket atom, can be adjusted using an *atom quantifier*. Atom quantifiers define *atom sequences*, that is, matches occur when a contiguous repetition for the atom is found in the string. The substring corresponding to the match is called a piece. Notwithstanding, quantifiers and other features of regular expressions are treated differently depending on which standard is being used.

As defined by POSIX, there are two forms of regular expressions: “basic” regular expressions and “extended” regular expressions. Most text related programs in any conventional Linux distribution support both forms, so it is important to know their differences in order to avoid compatibility issues and to pick the most suitable implementation for the intended task.

The * quantifier has the same function in both basic and extended REs (atom occurs zero or more times) and it’s a literal character if it appears at the beginning of the regular expression or if it’s preceded by a backslash \ . The plus sign quantifier ` + `will select pieces containing one or more atom matches in sequence. With the question mark quantifier `?` , a match will occur if the corresponding atom appears once or if it doesn’t appear at all. If preceded by a backslash `\` , their special meaning is not considered. Basic regular expressions also support `+` and `?` quantifiers, but they need to be preceded by a backslash. Unlike extended regular expressions, + and ? by themselves are literal characters in basic regular expressions.

### Bounds

A *bound* is an atom quantifier that, as the name implies, allows a user to specify precise quantity boundaries for an atom. In extended regular expressions, a bound may specify in three forms:

```
{i}
```

The atom must appear exactly i times (i an integer number). For example, [[ :blank:]]{2} matches with exactly two blank characters.

```
{i,}
```

The atom must appear at least i times (i an integer number). For example, [[ :blank:]]{2,} matches with any sequence of two or more blank characters.

```
{i,j}
```

The atom must appear at least i times and at most j times (i and j integer numbers, j greater then i). For example, x y z{2,4} matches the x y string followed by two to four of the z character.

In any case, if a substring matches with a regular expression and a longer substring starting at the same point also matches, the longer substring will be considered.

Basic regular expressions also support bounds, but the delimiters must be preceded by \: \{ and \}. By themselves, { and } are interpreted as literal characters. A \{ followed by a character other
