
## ASTERISKS

An asterisk can follow a regular expression that represents a single character (Table A-4). The asterisk represents *zero* or more occurrences of a match of the regular expression. An asterisk following a period matches any string of characters. (A period matches any character, and an asterisk matches zero or more occurrences of the preceding regular expression.) A character-class definition followed by an asterisk matches any string of characters that are members of the character class.

| **Regular expression** | **Matches** | **Examples** |
| :--- | :--- | :--- |
| /\*ab\*c/ | a followed by zero or more b’s followed by a c | ac, abc, abbc, debcaabbbc |
| /ab\*\*c/ | ab followed by zero or more characters followed by c | abc, abxc, ab45c, xab 756 345 x cat |
| /\*.ing/ | t followed by zero or more characters followed by ing | thing, ting, I thought of going |
| /[a-zA-Z ]\*./ | A string composed only of letters and SPACES | 1. any string without numbers or punctuation! |
| /(.\*}/ | As long a string as possible between { and } | Get {this} and {that}; |
| /[^{\*}\*}/ | The shortest string possible that starts with { and ends with } | {this}, Get {this and that} |

## CARETS AND DOLLAR SIGNS

A regular expression that begins with a caret (^) can match a string only at the beginning of a line. In a similar manner, a dollar sign ($) at the end of a regular expression matches the end of a line. The caret and dollar sign are called anchors because they force (anchor) a match to the beginning or end of a line (Table A-5).

| **Regular expression** | **Matches** | **Examples** |
| :--- | :--- | :--- |
| /^\*T/ | A T at the beginning of a line | This line... That Time... In Time |
| /^\*[0–9]f/ | A plus sign followed by a digit at the beginning of a line | +5 +45.72, +759 Keep this... |
| /:\$/ | A colon that ends a line | ...below; |

## QUOTING SPECIAL CHARACTERS

You can quote any special character (but not parentheses [except in Perl; page 1077] or a digit) by preceding it with a backslash (Table A-6). Quoting a special character makes it represent itself.

**Table A-6** Quoted special characters

| **Regular expression** | **Matches** | **Examples** |
| :--- | :--- | :--- |
| /end\./ | All strings that contain *end* followed by a period | The *end.*, *send.*, *pretend* *mail* |
| /\\/ | A single backslash | `\` |
| /\*/ | An asterisk | `*`, an asterisk (*) |
| /\[5\]/ | `[5]` | it was five [5] |
| /and/or/ | *and/or* | *and/or* |

## RULES

The following rules govern the application of regular expressions.

## LONGEST MATCH POSSIBLE

A regular expression always matches the longest possible string, starting as far toward the beginning of the line as possible. Perl calls this type of match a *greedy match* (page 1076). For example, given the string

```
This (rug) is not what it once was (a long time ago), is it?
```

the expression /Th.*is/ matches

```
This (rug) is not what it once was (a long time ago), is
```

and /(.*)/ matches

```
(rug) is not what it once was (a long time ago)
```

However, /([*\^}]*)/ matches

```
(rug)
```

Given the string

```
singing songs, singing more and more
```

the expression /s.*sing/ matches

```
singing songs, singing
```

and /s.*sing song/ matches

```
singing song
```

## EMPTY REGULAR EXPRESSIONS

Within some utilities, such as `vim` and `less` (but not `grep`), an empty regular expression represents the last regular expression that you used. For example, suppose you give `vim` the following Substitute command:

```
:s/mike/robert/
```

If you then want to make the same substitution again, you can use the following command:

```
:s//robert/
```

Alternatively, you can use the following commands to search for the string **mike** and then make the substitution

```
/mike/
:s//robert/
```

The empty regular expression `(/)` represents the last regular expression you used `(/mike/)`.

## BRACKETING EXPRESSIONS

You can use quoted parentheses, `\(` and `\)`, to *bracket* a regular expression. (However, Perl uses unquoted parentheses to bracket regular expressions; page 1077.) The string that the bracketed regular expression matches can be recalled, as explained in “Quoted Digit.” A regular expression does not attempt to match quoted parentheses. Thus a regular expression enclosed within quoted parentheses matches what the same regular expression without the parentheses would match. The expression `/\(rexp\)/` matches what `/rexp/` would match; `/a\(b*c\)/` matches what `/ab*c/` would match.

You can nest quoted parentheses. The bracketed expressions are identified only by the opening `\(`, so no ambiguity arises in identifying them. The expression `/\([a-z]\|[A-Z]*\)x/` consists of two bracketed expressions, one nested within the other. In the string `3 t dMNOIx7 1 u`, the preceding regular expression matches **dMNOIx**, with the first bracketed expression matching **dMNOIx** and the second matching **MNOR**.

## THE REPLACEMENT STRING

The `vim` and `sed` editors use regular expressions as search strings within Substitute commands. You can use the ampersand (`&`) and quoted digits (`\n`) special characters to represent the matched strings within the corresponding replacement string.

## AMPERSAND

Within a replacement string, an ampersand (&) takes on the value of the string that the search string (regular expression) matched. For example, the following vim Substitute command surrounds a string of one or more digits with NN. The ampersand in the replacement string matches whatever string of digits the regular expression (search string) matched:

```
:s/[0-9][0-9]*/\N&\N/
```

Two character-class definitions are required because the regular expression [0-9]* matches zero or more occurrences of a digit, and any character string constitutes zero or more occurrences of a digit.

## QUOTED DIGIT

Within the search string, a bracketed regular expression, \\ (xxxx) [\(xxx) in Perl], matches what the regular expression would have matched without the quoted parentheses, xxx. Within the replacement string, a quoted digit, \\u (u), represents the string that the bracketed regular expression (portion of the search string) beginning with the u th \\ matched. Perl accepts a quoted digit (for this purpose), but the preferred style is to precede the digit with a dollar sign ($n; page 1077). For example, you can take a list of people in the form

```
last-name, first-name initial
```

and put it in the form

```
first-name initial last-name
```

with the following vim command:

```
:1,$s/\(([\.\*\\\]), \([^\.,]\\\)/2 \1/
```

This command addresses all the lines in the file (1,$). The Substitute command (s) uses a search string and a replacement string delimited by forward slashes. The first bracketed regular expression within the search string, \([^.] *\\), matches what the same unbracketed regular expression, [^.] *\\, would match: zero or more characters not containing a comma (the last-name). Following the first bracketed regular expression are a comma and a SPACE that match themselves. The second bracketed regular expression, \\ (\\*\\), matches any string of characters (the first-name and initial).

The replacement string consists of what the second bracketed regular expression matched (\\2), followed by a SPACE and what the first bracketed regular expression matched (\\1).

## EXTENDED REGULAR EXPRESSIONS

This section covers patterns that use an extended set of special characters. These patterns are called *full regular expressions* or *extended regular expressions*. In addition to ordinary regular expressions, Perl and vim provide extended regular expressions. The three utilities egrep, grep when run with the -E option (similar to egrep), and mawk/gawk provide all the special characters included in ordinary regular expressions, except for \ (and \), as well those included in extended regular expressions.

Two of the additional special characters are the plus sign (+) and the question mark (?). They are similar to *, which matches zero or more occurrences of the previous character. The plus sign matches one or more occurrences of the previous character, whereas the question mark matches zero or one occurrence. You can use any one of the special characters *, +, and ? following parentheses, causing the special character to apply to the string surrounded by the parentheses. Unlike the parentheses in bracketed regular expressions, these parentheses are not quoted (Table A-7).

Table A-7 Extended regular expressions

In full regular expressions, the vertical bar (|) special character is a Boolean OR operator. Within vim, you must quote the vertical bar by preceding it with a backslash to make it special (\|). A vertical bar between two regular expressions causes a match with strings that match the first expression, the second expression, or both. You can use the vertical bar with parentheses to separate from the rest of the regular expression the two expressions that are being ORed (Table A-8).

Table A-8 Full regular expressions
