
This command inserts two lines of text at the beginning of novels, the file used in the previous examples in this section. This file would now contain the following:

```
The Novels of F. Scott Fitzgerald
--------------------------------
This Side of Paradise
The Beautiful and Damned
The Great Gatsby
Tender Is the Night
The Last Tycoon
```

## 11.7 Including Text Files

```
@sf(Debian): `m4'
```

File inclusion is where the contents of a file can be included at a particular place within some other file, just by specifying the file's name at that place in the other file.

This is useful if you want or need to frequently rearrange divisions or sections of a document, if you need to keep a document in more than one arrangement, or if you have some sections of text that you frequently insert in more than one document. For these situations, you can keep each section in a separate file and build an include file that contains the file names for the various sections in the order you want to generate that file.

To include a file in a text file, specify the file to be included on a line of its own, like this:

```
include(`file')
```

When you process this file for inclusion, the line with the `include' statement is replaced with the contents of the file file (whose path is relative to the current directory of the include file).

Use the m4 tool, the GNU macro processor, to process an include file. It takes as an argument the name of the include file, and it outputs the inclusion to the standard output. You can use redirection to redirect the output to a file.

For example, suppose the file `soups' contains this text:

```
Clam Chowder
Lobster Bisque
Vegetable
```

And suppose the file `sandwiches' contains this text:

```
BLT
```

And finally, suppose the file `menu` contains this text:

```
Ham on Rye
Roast Beef
```

```
Diner Menu For Today

Soups
-----

include(soups)

Sandwiches
------------

include(sandwiches)
```

- To process the file and write to the file `monday.txt`, type:

```
$ m4 menu > monday.txt
```

This command writes a new file, `monday.txt`, which looks like this:

```
Diner Menu For Today

Soups
-----

Clam Chowder
Lobster Bisque
Vegetable

Sandwiches
------------

BLT
Ham on Rye
Roast Beef
```

*NOTE:* You can write more than one include file that will use your files—and the files themselves can have include files of their own.

This is a fairly simple use of m4; it can do much more, including run commands, manipulate text, and run custom macros. See Info file `m4.info`, node `Top` for more information on this tool.

## The Linux Cookbook: Tips and Techniques for Everyday Use:

[ < ] [ > ]   [ << ] [ Up ] [ >> ]   [Top] [Contents] [Index] [ ? ]

## 12. Grammar and Reference

The tools and resources for writing and editing on Linux-based systems include spell checkers, dictionaries, and reference files. This chapter shows methods for using them.

- 12.1 Spelling
- 12.2 Dictionaries
- 12.3 Checking Grammar
- 12.4 Word Lists and Reference Files

Spell checking.
Grammar tools.
Word lists and reference files.

### 12.1 Spelling

There are several ways to spell check text and files on Linux; the following recipes show how to find the correct spellings of particular words and how to perform batch, interactive, and Emacs-based spell checks.

The system dictionary file, `/usr/dict/words` is nothing more than a word list (albeit a very large one), sorted in alphabetical order and containing one word per line. Words that are correct regardless of case are listed in lowercase letters, and words that rely on some form of capitalization in order to be correct (such as proper nouns) appear in that form. All of the Linux spelling tools use this text file to check spelling; if a word does not appear in the dictionary file, it is considered to be misspelled.

> NOTE: None of the computerized spell-check tools will correct your writing if you are using the wrong word to begin with---for example, if you have `there` when you mean `their`, the computer will not catch it (yet!).

- 12.1.1 Finding the Correct Spelling of a Word
- 12.1.2 Listing the Misspellings in a Text
- 12.1.3 Keeping a Spelling Word List
- 12.1.4 Interactive Spell Checking
- 12.1.5 Spell Checking in Emacs

Spell checking a word.
Spell checking a file.
Keeping a personal dictionary.
Interactive spell checking.
Spell checking in Emacs.
