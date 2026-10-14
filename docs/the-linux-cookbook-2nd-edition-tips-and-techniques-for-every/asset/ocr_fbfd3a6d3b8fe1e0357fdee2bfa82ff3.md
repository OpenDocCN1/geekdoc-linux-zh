word they should rhyme with (see Recipe 14.4.2 [Matching Lines Ending with Certain Text], page 343).

⇒ To output a list of words that rhyme with “friend,” search /usr/dict/words for lines ending with “end”:

```
$ grep 'end$' /usr/dict/words [RET]
```

Finally, to do a search on the WordNet dictionary, use wn with one of the -grep options. When you give some text to search for as an argument, this command does the equivalent search as look, but only the particular kind of word sense you specify is searched: -grepn searches nouns, -grepv searches verbs, -grepa searches adjectives, and -grepr searches adverbs. You can combine options to search multiple word senses.

⇒ Here are two ways to use this.

+   - To search the WordNet dictionary for nouns that begin with “homew,” type:

```
$ wn homew -grepn [RET]
```

+   - To search the WordNet dictionary for both nouns and adjectives that begin with “homew,” type:

```
$ wn homew -grepn -grepa [RET]
```

# 11.2.2 Listing the Definitions of a Word

To list the definitions of a word, give the word as an argument to wn, followed by the -over option.

⇒ To list the definitions of the word “slope,” type:

```
$ wn slope -over [RET]
```

NOTES: If you look up dictionary definitions frequently enough, it is handy to have an alias of “def” defined as wn $1 -over (see Recipe 3.6.1 [Calling a Command by Some Other Name], page 83).

# 11.2.3 Listing the Synonyms of a Word

A synonym of a word is a different word with a similar meaning that can be used in place of the first word in some context. To output synonyms for a word with wn, give the word as an argument, followed by one of the following options: -synsn for nouns, -synsv for verbs, -synsa for adjectives, or -synsr for adverbs.