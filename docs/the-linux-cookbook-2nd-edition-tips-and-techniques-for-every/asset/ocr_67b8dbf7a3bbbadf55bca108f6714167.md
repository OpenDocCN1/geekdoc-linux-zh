# 10.7 Including Text from Other Files

M4
DEB: m4
RPM: m4
WWW: http://www.gnu.org/software/m4/m4.html

File inclusion is when the content of a file is included at a particular place within some other file, just by specifying the file's name at that place in the other file.

This is useful if you want or need to frequently rearrange divisions or sections of a document, if you need to keep a document in more than one arrangement, or if you have some sections of text that you frequently insert in more than one document. For these situations, you can keep each section in a separate file and build an include file that contains the file names of the various sections in the order you want for that file.

To include a file in a text file, specify the file to be included on a line of its own, like this:

```
include(file)
```

When you process this file for inclusion, the line with the "include" statement is replaced with the contents of the file file (whose path is relative to the current directory of the include file).

Use the m4 tool, the GNU macro processor, to process an include file. It takes as an argument the name of the include file, and it outputs the inclusion to the standard output. You can use redirection to redirect the output to a file.

For example, suppose you have three files: soups as in Figure 10-9, sandwiches as in Figure 10-10, and menu as in Figure 10-11.

![](bbox=[0.22, 0.78, 0.88, 0.88])

Figure 10-9. The soups file.

6 This is a fairly simple use of m4; it can do much more, including run commands, manipulate text, and run custom macros. Consult its Info documentation for more (see Recipe 2.8.5 [Reading an Info Manual], page 48).