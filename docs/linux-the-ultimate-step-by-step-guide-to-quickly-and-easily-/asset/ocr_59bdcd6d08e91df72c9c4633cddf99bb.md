| `[:xdigit:]` | Hex digits [0-9 a-f A-F] | – |

```
$ sed -e ‘s/^[[[:digit:]][[[:digit:]][[[:digit:]]/(&)/g’ phone.txt

(555)5551212
(555)5551213
(555)5551214
(666)5551215
(666)5551216
(777)5551217
```

Here you are matching the first 3 digits and then using & replacing those 3 digits with surrounding parentheses.

# Using Multiple sed Commands

You can use multiple $sed$ commands in a single $sed$ command as follows –

```
$ sed -e ‘command1’ -e ‘command2’ ... -e ‘commandN’ files
```

Here $command_1$ through $command_N$ are $sed$ commands of the type discussed previously. These commands are applied to each line in the list of files given by files. Using the same mechanism, we can write above phone number example as follows –

```
$ sed -e ‘s/^[[[:digit:]][{3}\]/(&)/g’ \

-e ‘s/][[:digit:]]{3}/&-/g’ phone.txt

(555)555-1212
(555)555-1213
(555)555-1214
(666)555-1215
(666)555-1216
(777)555-1217
```

**Note** – In the above example, instead of repeating the character class keyword `[[digit:]]` three times, you replaced it with `\{3\}`, which means to match the preceding regular expression three times. Here I used `\\` to give line break you should remove this before running this command.

# Back References

The ampersand metacharacter is useful, but even more useful is the ability to define specific regions in a regular expression so you can reference them in your replacement strings. By defining specific parts of a regular expression, you can then refer back to those parts with a special reference character. To do back references, you have to first define a region and then refer back to that region. To define a region you insert backslash parentheses around each region of interest. The first region that you surround with backslashes is then referenced by `\\1`, the second region by `\\2`, and so on.