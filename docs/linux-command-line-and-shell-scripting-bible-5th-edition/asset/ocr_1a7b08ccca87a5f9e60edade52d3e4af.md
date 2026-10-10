# Part III: Advanced Shell Scripting

```
$ echo "ieek" | sed -n '/ie*\k/p'
ieek
$ echo "ieeek" | sed -n '/ie*\k/p'
ieeek
$ echo "ieeeek" | sed -n '/ie*\k/p'
ieeeek
$
```

This pattern symbol is commonly used for handling words that have a common misspelling or variations in language spellings. For example, if you need to write a script that may be used in either American or British English, you could write:

```
$ echo "I'm getting a color TV" | sed -n '/colou*\r/p'
I'm getting a color TV
$ echo "I'm getting a colour TV" | sed -n '/colou*r\r/p'
I'm getting a colour TV
$
```

The u* in the pattern indicates that the letter u may or may not appear in the text to match the pattern. Similarly, if you know of a word that is commonly misspelled, you can accommodate it by using the asterisk:

```
$ echo "I ate a potatoes with my lunch." | sed -n '/potatoe*\p/'
I ate a potatoes with my lunch.
$ echo "I ate a potato with my lunch." | sed -n '/potato*\p/'
I ate a potato with my lunch.
$
```

Placing an asterisk next to the possible extra letter allows you to accept the misspelled word.

Another handy feature is combining the dot special character with the asterisk special character. This combination provides a pattern to match any number of any characters. It’s often used between two text strings that may or may not appear next to each other in the data stream:

```
$ echo "this is a regular pattern expression" | sed -n '\/regular.*expression\/'
this is a regular pattern expression
```

Using this pattern, you can easily search for multiple words that may appear anywhere in a line of text in the data stream.

The asterisk can also be applied to a character class. Doing so allows you to specify a group or range of characters that can appear more than once in the text:

```
$ echo "bt" | sed -n '\\b[ae]*t\\p'
bt
$ echo "bat" | sed -n '\\b[ae]*t\\p'
bat
$ echo "bet" | sed -n '\\b[ae]*t\\p'
bet
```