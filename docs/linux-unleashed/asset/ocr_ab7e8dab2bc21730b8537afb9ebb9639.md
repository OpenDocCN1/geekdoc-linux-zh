```
\def\mistake#1{This is wrong because of #2.}
```

is incorrect because it refers to a second parameter that is not specified in the formal parameter list.

Macros can be redefined in your document, but you should be aware that only the most recent definition will be applied. Also, macros defined within groups are valid only within the scope of the group.

Macro definitions can be nested one within another, as in the following:

```
\def\hey{Hey\def\hey{hey}}
\hey, \hey, \hey.
```

This has the following output:

Hey, hey, hey.

As with many topics within this book, we have examined only some of the highlights of TeX. There is much more to learn but, having covered the basics regarding macros, you can now look at the most popular extension of TeX, which uses macros to enhance the creation of documents. This extension is LaTeX.

# # LaTeX: An Enhancement of TeX

LaTeX is a collection of macros that build on the capabilities of TeX and provide a higher level of abstraction for the creation of documents. It is essentially a style library that encourages uniform formatting and typesetting across documents. LaTeX macros shift the emphasis away from the details of things such as “set text to 8-point slanted” to concepts that writers identify more readily with, such as the emphasis of a word or phrase. Thus, LaTeX macros have names that are more representative of the way writers *think* when they are writing.

Because LaTeX is an extension of TeX, you’ll find it easy to become quickly productive in LaTeX, assuming that you have some experience in TeX. Whitespace and spacing between paragraphs are handled in the same manner as in TeX. The special characters in TeX are the same in LaTeX, and comments are denoted using the % character.

The key differences between TeX and LaTeX become apparent as you learn more about the macros that define the layout of your document in a convenient fashion.