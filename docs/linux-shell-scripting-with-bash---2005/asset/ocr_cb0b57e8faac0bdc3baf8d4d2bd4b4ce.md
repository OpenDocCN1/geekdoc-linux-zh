# ## Dollar Sign Substitutions

The dollar sign is used for more than variable substitution. There are a variety of dollar expansions, some substituting string values and others mimicking capabilities of Linux commands such as `wc` and `sed`. By using the dollar sign expressions, the shell doesn’t have to start these programs and will run faster.

# ### ANSI C Escape Expansion (\$‘ )

If a dollar sign is followed by a string in single quotes, the string is searched for ANSI C escape sequences and the sequences are replaced by the corresponding characters. The acceptable escape sequences are similar to the special format escape codes used by the `printf` command:

+   * `\a`—Alert (bell)
+   * `\b`—Backspace
+   * `\cC`—A control character *C* (for example, G for control-G)
+   * `\e`—Escape character
+   * `\f`—Form feed
+   * `\n`—New line
+   * `\r`—Carriage return
+   * `\t`—Horizontal tab
+   * `\v`—Vertical tab
+   * `\\`—A literal backslash
+   * `\’`—A single quote
+   * `\nnn`—The ASCII octal value for a character (up to three digits)
+   * `\xnnn`—The ASCII hexadecimal value for a character (up to three digits)

```
$ `printf "%a\n" '$'\nline 2\newline 3'`
line 1
line 2
line 3
```

# ### Locale Translation (\$‘ ‘ )

If a dollar sign is followed by a string in double quotes, the string is translated into the character set of the current locale.

```
$ `printf "'%a\n' 'To a new locale'"
To a new locale
```

Locales are discussed briefly in Chapter 18, “Final Topics.”