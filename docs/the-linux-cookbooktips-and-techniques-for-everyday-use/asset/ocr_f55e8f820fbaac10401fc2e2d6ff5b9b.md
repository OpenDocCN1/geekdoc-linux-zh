# 11.2.3 Making Abbreviations in Emacs

An abbrev is a word that is an abbreviation of a (usually) longer word or phrase. Abbrevs exist as a convenience to you—you can define abbrevs to expand to a long phrase that is inconvenient to type, or you can define a misspelling that you tend to make to expand to its correct spelling. Abbrevs only expand when you have Abbrev mode enabled.

+   - To turn on Abbrev mode, type:

```
M-x abbrev-mode RET
```

To define an abbrev, type the abbrev you want to use and then type C-x a i g. Emacs will prompt in the minibuffer for the text you want the abbrev to expand to; type that text and then type RET.

+   - To define `rbf' as an abbrev for `R. Buckminster Fuller', do the following:

+   - First, type the abbrev itself:

```
rbf
```

+   - Next, specify that this text is to be an abbrev; type:

```
C-x a i g
```

+   - Now type the text to expand it to:

```
Global expansion for "rbf": R. Buckminster Fuller RET
```

Now, whenever you type `rbf' followed by a whitespace or punctuation character in the current buffer, that text will expand to the text `R. Buckminster Fuller'.

To save the abbrevs you have defined so that you can use them later, use the write-abbrev-file function. This saves all of the abbrevs currently defined to a file that you can read in a future Emacs session. (You can also open the file in a buffer and edit the abbrevs if you like.)