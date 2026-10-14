⇒ To output all lines in playlist that contain both patterns “the sea” and “cake,” regardless of case, type:
$ grep -i 'the sea' playlist | grep -i cake [RET]

NOTES: To match lines containing some regexps in a particular order, see Recipe 14.3.6 [Using Popular Regexps for Common Situations], below.

# 14.3.4 Matching Lines That Don’t Contain a Regexp

To output all lines in a text that don’t contain a given pattern, use grep with the -v option—this option reverses the sense of matching, selecting all non-matching lines.

+   ⇒ Here are two ways to use this.
+   - To output all lines in /usr/dict/words that are not three characters wide, type:
+     $ grep -v '..'..'..' [RET]
+   - To output all lines in access_log that do not contain the string "http", type:
+     $ grep -v http access_log [RET]

# 14.3.5 Matching Lines That Only Contain Certain Characters

To match lines that only contain certain characters, use the regexp “^[characters]*$,” where characters lists the ones to match.

⇒ To output lines in /usr/dict/words that only contain vowels, type:
$ grep -i '^[aeiou]*$' /usr/dict/words [RET]

The -i option matches characters regardless of case; so, in this example, all vowel characters are matched regardless of case.

# 14.3.6 Using Popular Regexps for Common Situations

The following table lists sample regexps and describes the lines that they match. Use these regexps as boilerplate when building your own regular expressions for searching text. Remember to type regexps all on one line, and to quote them (see Recipe 3.1.3 [Quoting Reserved Characters], page 56).