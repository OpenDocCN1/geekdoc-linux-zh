# 15.2.5 Matching Lines That Contain All of Some Regexps

To output lines that match all of a number of regexps, use grep to output lines containing the first regexp you want to match, and pipe the output to a grep with the second regexp as an argument. Continue adding pipes to grep searches for all the regexps you want to search for.

+   - To output all lines in `playlist` that contain both patterns `the sea` and `cake`, regardless of case, type:

```
$ grep -i 'the sea' playlist | grep -i cake RET
```

NOTE: To match lines containing some regexps in a particular order, see Regexps for Common Situations.

# 15.2.6 Matching Lines That Don't Contain a Regexp

To output all lines in a text that don't contain a given pattern, use grep with the `-v` option—this option reverts the sense of matching, selecting all non-matching lines.

+   - To output all lines in `/usr/dict/words` that are not three characters wide, type:

```
$ grep -v '^...$' RET
```

+   - To output all lines in `access_log` that do not contain the string `http`, type:

```
$ grep -v http access_log RET
```

# 15.2.7 Matching Lines That Only Contain Certain Characters

To match lines that only contain certain characters, use the regexp `^[characters]*$`, where characters are the ones to match.