approach to formatting TeX documents. TeX and LaTeX tools are contained in the texlive-latex package.

TeX interprets the LaTeX macros from the latex format file (`latex.fmt`). By default, the `latex.fmt` and `plain.fmt` format files are the only ones that are built automatically when the TeX package is installed. Other macro files you can use with TeX include:

+   *   **amstex** — Mathematical publications, including the American Mathematical Society use this as their official typesetting system.
+   *   **explain** — Includes macros for indexing and table of contents.
+   *   **texinfo** — Macros used by the Free Software Foundation to produce software manuals. Text output from these macros can be used with the `Linux info` command.

You can create a TeX/LaTeX file using any text editor. After the text and macros are created, you can run the `tex` command (or one of several other related utilities) to format the file. The input file is in the form `filename.tex`. The output is generally three different files:

+   *   `filename.dvi` — This is the device-independent output file that can be translated for use by several different types of output devices (such as PostScript).
+   *   `filename.log` — This is a log file that contains diagnostic messages.
+   *   `filename.aux` — This is an auxiliary file used by LaTeX.

The `.dvi` file produced can be formatted for a particular device. For example, you could use the `dvips` command to output the resulting `.dvi` file to your PostScript printer (`dvips filename.dvi`). Or you could use the `xdvi` command to preview the `.dvi` file in X.

# ### Creating and formatting a LaTeX document

The best way to get started with LaTeX is to use the LyX editor. LyX provides a GUI for creating LaTeX documents. It also contains a variety of templates you can use instead of just creating a document from scratch. Figure 6-7 shows an example of the LyX editor.

> **NOTE:** The LyX editor is available from the Fedora repository; you can install it by typing `yum install lyx`.

If you want to edit LaTeX in a regular text editor, you need to be familiar with the LaTeX commands. For a complete listing of the LaTeX commands, type `info latex` and then go to the section “Commands within a LaTeX document.”

# ### Converting documents

Documents can come to you in many different formats. Search just some of the Linux FTP sites on the Internet and you will find files in PostScript, DVI, man, PDF, HTML, and TeX. There are also a variety of graphics formats. Fedora comes with lots of utilities to convert documents and graphics from one format to another. The following is a list of document and graphics conversion utilities: