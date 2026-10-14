# 12.1.4 Interactive Spell Checking

Use ispell to spell check a file interactively, so that every time a misspelling is found, you're given a chance to replace it then and there.

+   To interactively spell check `fall-lecture.notes`, type:

```
$ ispell fall-lecture.notes RET
```

When you type this, ispell begins checking the file. It stops at the first misspelling it finds:

```
lecutres          File: fall-lecture.notes

The focus of my series of lecutres this fall are the aspects of the novel.

0: lectures
```

```
[SP] <number> R)epl A)ccept I)nsert L)ookup U)ncap Q)uit e(X)it or ? for help
```

On the top line of the screen, ispell displays the misspelled word, followed by the name of the file. Underneath this is the sentence in which the misspelling appears, with the word in question highlighted. Following this is a list of suggested words, each offset by a number---in this example, ispell has only one suggestion: `lectures`.

To replace a misspelling with a suggested word, type the number that corresponds to the suggested word (in this example, you would type 0 to replace the misspelling with `lectures`). You only need to type the number of your selection---a RET is not required.

You can also type a correction yourself: this is useful when ispell either offers no suggestions, or when it does and the word you want is not one of them. To do this, type x (for "replace") and then type the replacement word, followed by RET.

Sometimes, ispell will question a word that you may not want to count as a misspelling, such as proper names and the like---words that don't appear in the system dictionary. There are a few things you can do in such cases, as follows.