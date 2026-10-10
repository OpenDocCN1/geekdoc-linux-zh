![](bbox=[0.08, 0.15, 0.13, 0.26])

In LaTeX jargon, an environment is the category of text between two defining tags. This includes lists, quotations, various mathematical forms, tables, and many others. Environments can be nested. For example, the outermost environment is the document class, which sets parameters for the entire document, such as what subsections are valid. This book’s document class uses chapters for subsections, whereas an article uses sections. Many LaTeX environments are analogous to the various HTML tags, although LaTeX has many more possibilities.

LaTeX files need a few basic tags in order to be valid. The first is the document class tag, which lets TeX know whether the file is intended to be a book, an article, or a report. Immediately following a backslashed tag can be a statement in curly brackets. This can be a section or chapter name or any variable value that might apply to a tag. Think of them as the arguments to a formatting command.

The actual content of your chapter or section is typed like any other text. You don’t need to worry about formatting, because TeX does this for you when you process the file. There are things you need to keep in mind while writing this type of file. Eight characters have a special meaning to the TeX program, and they can’t be inserted literally unless you precede them with a backslash:

```
$
&
%
{
}
]\\
^
```

For example, if you needed a numerical dollar amount in a file, you would write $\$2.00. The backslash is an exception to this rule, because \textbackslash{}\textbackslash{} is defined as the “force a new line” command. To insert a backslash in a file, you need to write it like this:

```
\backslash
```

Another possible source of errors to keep in mind is that all “begin” tags must be balanced by an “end” tag, and all curly brackets must be in matched pairs. AUCTeX helps you keep track of these, because it always inserts both beginning and ending tags when you use the menu or keybindings to insert environment tags.

Here is something else to try in your new file. Select List from the Insert Environment submenu. A pair of tags defining a list appears in your buffer, along with the first “item” tag, and your cursor will be where it needs to be so that you can easily write the list item. Write something there, and then press M-Enter. A new list