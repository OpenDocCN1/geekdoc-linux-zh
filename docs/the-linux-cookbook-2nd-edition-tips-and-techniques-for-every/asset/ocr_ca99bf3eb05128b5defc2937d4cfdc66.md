⇒ Here are two ways to use this.

+   - To output all of the synonyms for the noun “break,” type:
+     $ wn break -synsn [RET]

+   - To output all of the synonyms for the verb “break,” type:
+     $ wn break -synsv [RET]

# 11.2.4 Listing the Antonyms of a Word

An antonym of a word is a different word that has the opposite meaning of the first in some context. To output antonyms for a word with wn, give the word as an argument, followed by one of the following options: -antsv for verbs, -antsa for adjectives, or -antar for adverbs.

⇒ To output all of the antonyms for the adjective “sad,” type:

```
$ wn sad -antsa [RET]
```

# 11.2.5 Listing the Hypernyms of a Word

A hypernym of a word is a related term whose meaning is more general than the given word. (For example, the words “mammal” and “animal” are hypernyms of the word “cat.”)

To output hypernyms for a word with wn, use one of the following options: -hyper for nouns or -hypev for verbs.

⇒ To output all of the hypernyms for the noun “cat,” type:

```
$ wn cat -hyper [RET]
```

# 11.2.6 Checking Online Dictionaries

Dict
DEB: dict
RPM: dict
WWW: http://www.dict.org/

The DICT Development Group has a number of free dictionaries on its Web site [http://www.dict.org/]. On that page, you can look up words (including using a thesaurus and other searches) from a dictionary that contains over 300,000 headwords, or you can make a copy of its dictionary for use on your own system. A dict client exists for accessing DICT servers and outputting definitions locally; this tool is available in the dict package.