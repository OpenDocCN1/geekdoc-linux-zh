# 12.2 Listing Words in Text

When analyzing text, a “word” can be any grouping of characters that are separated from other words by either blank spaces or newlines. They can be English words, numbers, symbols, and so on.

Making a listing of the words that appear in some text—either a file or standard input—is a simple matter when you use a popular combination of tr, sort, and uniq, all tools for formatting text that are discussed in the next chapter (see Chapter 13 [Formatting Text], page 305).

You can sort these lists alphabetically, remove any duplicate words, and list the frequency each word appears in the original text. These alphabetical word-frequency lists are similar to a concordance, which is an index of all the words in a text, along with their contexts.

Since tr is a filter, these recipes use redirection to send files to tr’s standard input (see Recipe 3.2.1 [Redirecting Input to a File], page 67). The output is usually piped to less for perusal. If you want to print or peruse the output of these recipes, I recommend you pipe them to pr to paginate the output and place it in columns (see Recipe 13.3 [Paginating Text], page 312). A further refinement is to use enscript to print them in a nice font (see Recipe 15.2.1 [Outputting Text in a Font], page 361).

# 12.2.1 Listing All of the Words in Text

To output a list of all of the words as they appear in some text, use the tr filter to translate all horizontal whitespace (such as tab and space characters) to newline characters, and squeeze out blank lines.

+   ⇒ To peruse a list containing all of the words from the text file book as they appear in the text, type:

```
$ tr -s '[[:blank:]]' '\n' < book | less RET
```

+   ⇒ To remove all of the punctuation from the listed words, pipe the output to another tr that deletes it.

+   ⇒ To peruse a list containing all of the words from the text file book as they appear in the text, but with punctuation removed, type:

```
$ tr -s '[[:blank:]]' '\n' < book | tr -d '[[:punct:]]' | less RET
```

Dashes are not removed with punctuation. If the text to filter contains em dashes consisting of two hyphens (--) with no spaces between the words on either side of the dashes, first filter them out by with SED, replacing them with a space character (see Recipe 10.5 [Editing Streams of Text], page 255). Then pass that filtered text to tr.