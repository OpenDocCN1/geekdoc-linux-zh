# Formatting Text with TeX

The TeX typesetting system, originally by Donald E. Knuth, is a collection of programs and other utilities used to produce professionally formatted documents. It is a much more sophisticated system than the groff distribution and includes more than 65 programs, along with such related support files as libraries, macros, fonts, and documentation.

If you install TeX on your system with the lisa or rpm commands, you need at least 30 megabytes for the main distribution, 10 megabytes for a series of related macros called LaTeX, and eight megabytes for 50 different fonts. Obviously, describing the entire system and how to use each different program in the TeX system is beyond this hour. But this section shows you how to get started with a sample document.

![](bbox=[0.3, 0.55, 0.35, 0.65])

> Previewing TeX dvi documents requires a preprocessing step that can take several minutes before the pages are even displayed. Files must first be processed by the MakeTeXPK program, and related processes can eat up your system resources. A much better approach is to convert the file to PostScript with the dvips command, found under the /usr/bin directory with the following:
> Now use the gv program with gv tex.ps to read the file.

```
dvips -f < texdoc.dvi >tex.ps
```

You can find documentation for TeX in a variety of places. You can read the manual pages for related files, check the /usr/info directory for TeX information files, and browse to the /usr/TeX/texmf/doc directory. There are 10 different directories of documentation files, but the easiest way to read about your TeX distribution is to use the lynx Web browser with the following:

```
# lynx ls /usr/TeX/texmf/doc/index.html
```

The TeX distribution files are displayed in an organized list that you can browse through to download sample files and guides directly to your home directory. Beginning users should definitely read the TeX Frequently Asked Questions (FAQ) document.

Like the groff program, TeX uses formatting commands inserted in your text files to manipulate how your file looks when printed. You create your file, insert appropriate commands or macros to format text, and then process your document through TeX to create an output file, usually in dvi format, that you can preview or print.

To see a sample of TeX using the LaTeX macros, try processing a sample file in the TeX directories: