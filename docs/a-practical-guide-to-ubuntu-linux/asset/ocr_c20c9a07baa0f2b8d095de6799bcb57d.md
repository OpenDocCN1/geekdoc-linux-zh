# CONVENTIONS USED IN THIS BOOK 19

download new software over the Internet quickly and reliably. Chapter 10 dis-
cusses networks, the Internet, and the Linux network facilities.

# SOFTWARE DEVELOPMENT

One of Linux's most impressive strengths is its rich software development environ-
ment. Linux supports compilers and interpreters for many computer languages.
Besides C and C++ languages available for Linux include Ada, Fortran, Java, Lisp,
Pascal, Perl, and Python. The bison utility generates parsing that makes it eas-
ier to write build compilers (that parse files containing struc-\ured information). The flex utility generates scanners (code that recognizes lexical
patterns in text). The make utility and the GNU Compiler and Build System make
it easier to manage complex development projects. Source code management syst-\ems, such as CVS, simple version control. Several debuggers, including ups and
gdb, can help you track down and repair software defects. The GNU C compiler
(gcc) works with the gprof profiling utility to help programmers identify potential
bottlenecks in a program performance. The C compiler includes options to-
form extensive checking of C code, making the code more portable and
reducing debugging time. Table B-4 on page 1104 lists some sites you can down-
load software from.

# CONVENTIONS USED IN THIS BOOK

This book uses conventions to make its explanations shorter and clearer. The fol-
lowing paragraphs describe these conventions.

+   * Widgets A widget is a simple graphical element that a user interacts with, such as a text box,
radio button, or combo box. When referring to a widget, this book specifies the
type of widget and its label. The term "tick" refers to mark the you in a check
box, sometimes called a check mark. For example, "put a tick in the check box
Run in terminal." See the glossary for definitions of various widgets.

+   * Tabs and frames Tabs allow to display sets of related information, one at a time. For
example, Figure 4-12 on page 114 shows the Appearance Preferences window, which
has four tabs; The Theme is highlighted. A frame isolates a set of information
within a window. See Figure 14-3 on page 551 for an example.

+   * Menu selection path The menu selection path is the name of or the location of the menu, fol-
owed by a colon, SPACE, and the menu selections separated by markers. The
entire menu selection path appears in bold type. You can read Main menu: System-
Preferences Appearance as "From the Main menu, select System; from System,
select Preferences; and then select Appearance."

+   * Text and examples The text is in this type, whereas examples are shown in a monospaced font (also
called a fixed-width font:

```
$ C practice
This is a small file I created
with a text editor.
```