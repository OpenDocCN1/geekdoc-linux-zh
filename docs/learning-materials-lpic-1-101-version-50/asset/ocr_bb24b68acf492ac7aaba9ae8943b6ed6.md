+   * **. (dot)**
+   Atom matches with any character.

+   * **^ (caret)**
+   Atom matches with the beginning of a line.

+   * **$ (dollar sign)**
+   Atom matches with the end of a line.

For example, the regular expression bc, composed by the literal atoms b and c, can be found in the string abcd, but can not be found in the string a1cd. On the other hand, the regular expression .c can be found in both strings abcd and a1cd, as the dot . matches with any character.

The caret and dollar sign atoms are used when only matches at the beginning or at the end of the string are of interest. For that reason they are also called anchors. For example, cd can be found in abcd, but ^cd can not. Similarly, ab can be found in abcd, but ab$ can not. The caret ^ is a literal character except when at the beginning and $ is a literal character except when at the end of the regular expression.

# ## Bracket Expression

There is another type of atom named *bracket expression*. Although not a single character, brackets [] (including their content) are considered a single atom. A bracket expression usually is just a list of literal characters enclosed by [], making the atom match any single character from the list. For example, the expression [1b] can be found in both strings abcd and a1cd. To specify characters the atom should not correspond to, the list must begin with ^, as in [^1b]. It is also possible to specify ranges of characters in bracket expressions. For example, [0-9] matches digits 0 to 9 and [a-z] matches any lowercase letter. Ranges must be used with caution, as they might not be consistent across distinct locales.

Bracket expression lists also accept classes instead of just single characters and ranges. Traditional character classes are:

+   * **[:alnum:]**
+   Represents an alphanumeric character.

+   * **[:alpha:]**
+   Represents an alphabetic character.

+   * **[:ascii:]**
+   Represents a character that fits into the ASCII character set.