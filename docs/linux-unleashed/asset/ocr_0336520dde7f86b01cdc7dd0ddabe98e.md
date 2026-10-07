# ## VirTeX and IniTeX

Two other \TeX -related programs work together but perform slightly different roles. The IniTeX program is used to create a \TeX format (.fmt) file containing font definitions and macros. The VirTeX program can then quickly load this precompiled format file, much more quickly than \TeX can. The command to use a format file is as follows:

```
$ virtex \&myformat sometexfile
```

The & character is necessary for VirTeX to recognize that it is loading a format file first; the & must be escaped using the \\ character so as not to confuse the shell. The difference between VirTeX and IniTeX is that VirTeX can't be used to create \TeX format files, but it executes much faster.

# ## Summary

\TeX is a document-formatting system for Linux that enables authors to produce their own high-quality publications. It produces documents that are portable among output devices such as printers or displays. \TeX supports many typographical features and is particularly well-suited to the formatting of correct mathematical notation. It has macros that can be used to enhance the power of its basic command set. LaTeX, one of the most popular extensions to \TeX, uses sophisticated macros to help you organize and typeset your documents based on its contents. From here, you can learn about:

+   Using gawk, a handy and quick programming language for advanced users and system administrators, in Chapter 25, “gawk.”

+   Using Perl, another programming language that is very popular for Web-based scripting in Chapter 28, “Perl.”

+   Using Smalltalk/X, an X-based implementation of the object-oriented programming language, in Chapter 31, “Smalltalk/X.”