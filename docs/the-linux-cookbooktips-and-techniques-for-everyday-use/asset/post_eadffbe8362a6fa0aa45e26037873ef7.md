
## 15.6 Searching Text in Emacs

The following sections show ways of searching for text in Emacs---incrementally, for a word or phrase, or for a pattern---and for searching and then replacing text.

- 15.6.1 Searching Incrementally in Emacs
- Searching incrementally.
- 15.6.2 Searching for a Phrase in Emacs
- Searching for a word or phrase.
- 15.6.3 Searching for a Regexp in Emacs
- Searching for a pattern.
- 15.6.4 Searching and Replacing in Emacs
- Replacing text in Emacs.

### 15.6.1 Searching Incrementally in Emacs

Type C-s to use the Emacs incremental search function. It takes text as input in the minibuffer and it searches for that text from point toward the end of the current buffer. Type C-s again to search for the next occurrence of the text you're searching for; this works until no more matches occur. Then, Emacs reports `Failing I-search' in the minibuffer; type C-s again to wrap to the beginning of the buffer and continue the search from there.

It gets its name "incremental" because it begins searching immediately when you start to type text, and so it builds a search string in increments---for example, if you want to search for the word `sunflower' in the current buffer, you start to type

```
C-s a
```

At that point Emacs searches forward through the buffer to the first `s' character, and highlights it. Then, as you type u, it searches forward to the first `su' in the buffer and highlights that (if a `u' appears immediately after the `s' it first stopped at, it stays where it's at, and highlights the `s' and the `u'). It continues to do this as long as you type and as long as there is a match in the current buffer. As soon as what you type does not appear in the buffer, Emacs beeps and a message appears in the minibuffer stating that the search has failed.

NOTE: You can also search and replace text in most text editors, including Emacs; see Searching and Replacing in Emacs.

```
M-x replace-regexp RET helpless RET helpful RET
```

To search for the next instance of the last string you gave, type C-s again; if you keep CTRL held down, every time you press the S key, Emacs will advance to the next match in the buffer.

This is generally the fastest and most common type of search you will use in Emacs.

You can do an incremental search through the buffer in reverse—that is, from point to the beginning of the buffer—with the isearch-backward function, C-r.

- To search for the text `moon` in the current buffer from point in reverse to the beginning of the buffer, type:

```
C-r moon
```

### 15.6.2 Searching for a Phrase in Emacs

Like grep, the Emacs incremental search only works on lines of text, so it only finds phrases on a single line. If you search for `hello, world` with the incremental search and the text `hello,` appears at the end of a line and the text `world` appears at the beginning of the next line, it won’t find it.

To find a multi-word phrase across line breaks, use the word-search-forward function. It searches for a phrase or words regardless of punctuation or spacing.

- To search forward through the current buffer for the phrase `join me`, type:

```
M-x word-search-forward RET join me RET
```

NOTE: The word-search-backward function does the same as word-search-forward, except it searches backward through the buffer, from point to the beginning of the buffer.

### 15.6.3 Searching for a Regexp in Emacs

Use the search-forward-regexp function to search for a regular expression from point to the end of the current buffer.

- To search forward through the current buffer for the regexp `@.*\.org`, type:

```
M-x search-forward-regexp RET @.*\.org RET
```

The keyboard accelerator for this command is M-C-s — on most keyboards, you press and release ESC and then hold down CTRL while you type s. To repeat the last regexp search you made, type M-C-s C-s; then, as long as you have CTRL held down, you can keep typing s to advance to the next match, just as you would with an incremental search.

> NOTE: There is a search-backward-regexp function that is identical but searches backward, from point to the top of the buffer.

### 15.6.4 Searching and Replacing in Emacs

To search for and replace text in Emacs, use the replace-regexp function. When you run this function, Emacs will ask for both the text or regexp to search for and the text to replace it with.

- To replace the text `day' with the text `night' in the current buffer, type:

```
M-x replace-regexp RET day RET night RET
```

This function is especially useful for replacing control characters with text, or for replacing text with control characters, which you can specify with C-q, the quoted-insert function (see section Inserting Special Characters in Emacs).

- To replace all the `^M' characters in the current buffer with regular linefeeds, type:

```
M-x replace-regexp RET C-q C-m RET C-q 012 RET RET
```

## 15.7 Searching Text in Less

There are two useful commands in less for searching through text: / and ?. To search forward through the text, type / followed by a regexp to search for; to search backward through the text, use ?.

When you do a search, the word or other regexp you search for appears highlighted throughout the text.
