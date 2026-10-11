For example, say your developers have come up with the perfect amortization program and you want to install it on the workgroup server for other systems to remotely mount and use. Because this is a third-party or custom application, the logical place for it is in /usr/local/appname, possibly with a link to the program binary in the /usr/local/bin directory (because that’s in the path).

> If given a choice between putting the software package **BIGPROG** in the */usr/local/BIGPROG* section and the */opt/BIGPROG* section, it’s hard to choose. Read any relevant exam question closely—the main difference being that the */opt* section is not considered to be shareable, whereas the */usr* section is often shared and mounted by client systems.

# # File Management Commands

A major section of the 101 exam is dedicated to how to run commands properly with the right options and arguments. As a good sysadmin, you’ll be expected to know how to create, delete, edit, set permissions on, display, move, copy, and determine the type of files and programs.

> You must be able to pick proper and working commands out of lists of possibilities, type in appropriate strings in fill-in-the-blank boxes, and in general show that you’ve run the programs and utilities in question.

# # Tips for Working with Linux Files

Because most users and sysadmins come from a Windows or other OS background, a quick set of recommendations for the less-experienced can be of help here:

+   * **Hidden files aren’t really hidden**—They just begin with a ., such as the *.bashrc* and *.bash_profile* files. These are not viewable by normal users with conventional commands and switches and aren’t deleted by commands such as rm -f *. *.

+   * **Filenames can contain multiple periods or no period characters**—The filenames this.is.a.long.file and thisisalongfile are perfectly reasonable and possible.

+   * **Spaces in filenames look nice, but are a pain to type**—Use a - or a . instead of spaces because it’s neater and easier than prefixing all spaces with a \. (To display a space in a filename, the system shows a space prefixed with a backslash.)