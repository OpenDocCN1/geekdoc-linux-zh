# 15.6 Searching Text in Emacs

The following sections show ways of searching for text in Emacs---incrementally, for a word or phrase, or for a pattern---and for searching and then replacing text.

+   15.6.1 Searching Incrementally in Emacs
+   Searching incrementally.
+   15.6.2 Searching for a Phrase in Emacs
+   Searching for a word or phrase.
+   15.6.3 Searching for a Regexp in Emacs
+   Searching for a pattern.
+   15.6.4 Searching and Replacing in Emacs
+   Replacing text in Emacs.

# 15.6.1 Searching Incrementally in Emacs

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