+   • **texinfo** — Macros used by the Free Software Foundation to produce software manuals. Text output from these macros can be used with the Linux `info` command.

You can create a TeX/LaTeX file using any text editor. After the text and macros are created, you can run the `tex` command (or one of several other related utilities) to format the file. The input file is in the form `filename.tex`. The output is generally three different files:

+   • **filename.dvi** — This is the device-independent output file that can be translated for use by several different types of output devices (such as PostScript).

+   • **filename.log** — This is a log file that contains diagnostic messages.

+   • **filename.aux** — This is an auxiliary file used by LaTeX.

The `.dvi` file produced can be formatted for a particular device. For example, you could use the `dvips` command to output the resulting `.dvi` file to your PostScript printer (`dvips filename.dvi`). Or you could use the `xdu` command to preview the `.dvi` file in X.

# ## Creating and formatting a LaTeX document

Because LaTeX is the most common way of using TeX, this section describes how to create and format a LaTeX document. A LaTeX macro (often referred to as a command) appears in a document in one of the two following forms:

+   • `\string[option][required]` — First there is a backslash (`\`), which is followed by a *string* of characters. (Replace *string* with the name of the command.) Optional arguments are contained in braces (`{}`), and required arguments are in brackets (`[]`).

+   • `!?[option][required]` — First there is a backslash (`\`), which is followed by a single character that is not a letter. (Replace `?` with the command character.) Optional arguments are contained in braces (`{}`), and required arguments are in brackets (`[]`).

Each command defines some action to be taken. The action can control page layout, the font used, spacing, paragraph layout, or a variety of other actions on the document. The minimum amount of formatting that a LaTeX document can contain is the following:

```

\documentclass{name}
\begin{document}
   TEXT GOES HERE!
\end{document}

```

You should replace `{name}` with the name of the class of document you are creating. Valid document classes include `article`, `book`, `letter`, `report`, and `slides`. The text for the file, along with your formatting commands, goes between the `begin` and `end` document commands.

The best way to get started with LaTeX is to use the LyX editor. LyX provides a GUI for creating LaTeX documents. It also contains a variety of templates you can use instead of just creating a document from scratch. Figure 6-10 shows an example of the LyX editor.