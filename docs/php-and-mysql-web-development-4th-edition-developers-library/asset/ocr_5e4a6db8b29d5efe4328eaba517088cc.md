# C.2 Functions

If the search mode is `IN BOOLEAN MODE`, search results are based purely on absence or presence of the search words without regard to how often they occur in the table. For boolean searches, words in the search string can be modified with the following operators to affect how the search is done:

+   - A leading `+` or `-` indicates that the word must be present or absent.

+   - A leading `<` or `>` decreases or increases a word's contribution to the relevance value calculation.

+   - A leading `~` negates a word's contribution to the relevance value calculation, but does not exclude rows containing the word entirely as `-` would.

+   - A trailing `*` acts as a wildcard operator. For example, `act*` matches `act`, `acts`, `action`, and so forth.

+   - A phrase search may be performed by surrounding the phrase within double quotes (*`phrase`*). For a match to occur, each word must be present together in the order given in the phrase.

+   - Parentheses group words into expressions. Parenthesized expressions can be nested.

Words with no modifiers are treated as optional in a boolean search, just as for natural language searches.

It's possible to perform a boolean-mode search in the absence of a `FULLTEXT` index, but this can be quite slow.

If the search mode is `WITH QUERY EXPANSION`, a natural language search is done once using the search string, and then again using the search string and the information from the first few most highly relevant matches from the original search. This enables rows with content related to the original search string to be found.

For more information on `FULLTEXT` searching, see Section 2.15, "Using `FULLTEXT` Searches."

+   - `MID(str,pos,len)`
+     `MID(str,pos)`

The three-argument form of `MID()` returns a substring of the string `str` beginning at position `pos` and `len` characters long. The two-argument form returns the substring beginning at `pos` to the end of the string. Returns `NULL` if any argument is `NULL`.

```
```MID('what a dull example',8,4)      -> 'dull'
MID('what a dull example',8)          -> 'dull example'```
```

`MID()` is actually a synonym for `SUBSTRING()` and can be used with any of the forms of syntax that `SUBSTRING()` allows.