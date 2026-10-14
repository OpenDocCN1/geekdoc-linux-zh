
⇒ For example, to check whether the word “occurance” is misspelled, type:

```
$ spell [RET]
occurance [RET]
occurance
[CTRL]-[D]
$
```

In this example, spell echoed the word “occurance.” meaning that this word was not in the system dictionary and therefore was quite likely a misspelling. Then, [CTRL]-[D] was typed to exit spell.

## 11.1.2 Listing the Misspellings in Text

To output a list of misspelled words in a file, give the name of the file to check as an argument to spell. Any misspelled words in the file are output, each on a line of its own and in the order that they appear in the file.

⇒ To spell-check the file fall-lecture.draft, type:

```
$ spell fall-lecture.draft [RET]
occurance
willl
occurance
$
```

In this example, three words are output: “occurance,” “willl,” and “occurance” again, meaning that these three words were found in fall-lecture.draft, in that order, and were not in the system dictionary (and so were probably misspelled). Note that the misspelling “occurance” appears twice in the file.

To correct the misspellings, you could then open the file in your preferred text editor and edit it. Later in this section, I’ll describe an interactive spell checker that allows you to correct misspellings as they are found. Still another option is to use a text editor with spell-checking facilities built in, such as Emacs.

⇒ To spell-check the file fall-lecture.draft, and output any possibly misspelled words to a file fall-lecture.spelling, type:

```
$ spell fall-lecture.draft > fall-lecture.spelling [RET]
```

In this example, the standard output redirection operator (>) is used to redirect the output to a file (see Recipe 3.2.2 [Redirecting Output to a File], page 68).

To output an alphabetical list of the misspelled words, pipe the output to sort; then pipe the sorted output to the uniq filter to remove duplicates from the list (uniq removes duplicate adjacent lines from its input, outputting the "unique" lines).

⇒ To output a sorted list of the misspelled words that are in the file fall-lecture.draft, type:

```
$ spell fall-lecture.draft | sort | uniq [RET]
```

## 11.1.3 Keeping a Spelling Word List

The stock American English dictionary installed with Linux-based systems includes over 45,000 words. However large that number may seem, a lot of words are invariably left out—including slang, jargon, and some proper names.

You can view the system dictionary as you would any other text file, but users never edit this file to add words to it.³ Instead, you add new words to your own personal dictionary, a file in the same format as the system dictionary, but kept in your home directory as the file ~/.ispell_default.⁴

A user can have his own personal dictionary; the spelling commands discussed in this chapter automatically use your personal dictionary, if you have one, in addition to the system dictionary.

You build your personal dictionary using the i and u options of ispell, which insert words into your personal dictionary. Use these options either with the stand-alone tool or with the various ispell Emacs functions (see Recipe 11.1.4 [Interactive Spell Checking], page 278, and Recipe 11.1.5 [Spell Checking in Emacs], page 280).

⇒ To find out how many words you have in your personal dictionary, type:

```
$ wc -l ~/.ispell_default [RET]
```

NOTES: You can also add (or remove) words by manually editing the file with a text editor, but take care to keep the list in alphabetical order!

> ³ If a word is reasonably universal, you may, of course, contact the global maintainers of venglish or other appropriate packages, and try to convince them that said word ought to be included.

> ⁴ On newer systems, this file is sometimes replaced by ~/.aspell_default.

Over time, personal dictionaries begin to look very personal, as a reflection of their owners; Gregory Cosmo Haun made a work of conceptual art by photographing the portraits of a dozen users superimposed with listings of their personal dictionaries [http://www.reed.edu/~cosmo/art/DictPort.html].

## 11.1.4 Interactive Spell Checking

GNU Aspell
DEB: aspell
RPM: aspell
WWW: http://aspell.net/

or

Ispell
DEB: ispell
RPM: ispell
WWW: http://fmg-www.cs.ucla.edu/geoff/ispell.html

Use ispell to spell check a file interactively, so that every time a misspelling is found, you’re given a chance to replace it then and there.⁵

⇒ To interactively spell-check fall-lecture.notes, type:
$ ispell fall-lecture.notes [RET]

When you type this, ispell begins checking the file. It stops at the first misspelling it finds, as in Figure 11-1.

On the top line of the screen, ispell displays the misspelled word, followed by the name of the file. Underneath this is the sentence in which the misspelling appears, with the word in question highlighted. Following this is a list of suggested words, each offset by a number—in this example, ispell has only one suggestion: “lectures.”

To replace a misspelling with a suggested word, type the number that corresponds to the suggested word (in this example, you would type 0 to replace the misspelling with “lectures”). You only need to type the number of your selection—a [RET] is not required.

> ⁵ aspell is designed to be a drop-in replacement for ispell, with greatly improved suggestion algorithms. If your system has aspell, use it instead; it otherwise works like ispell.
