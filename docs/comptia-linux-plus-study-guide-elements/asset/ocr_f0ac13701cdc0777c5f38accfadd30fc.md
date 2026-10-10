| Section Number | Description |
| --- | --- |
| 1 | Executable programs and shell commands |
| 2 | System calls provided by the kernel |
| 3 | Library calls provided by program libraries |
| 4 | Device files (usually stored in /dev) |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous (macro packages, conventions, and so on) |
| 8 | System administration commands (programs run mostly or exclusively by root) |
| 9 | Kernel routines |

The convention for man pages is a succinct style that employs several sections. Common sections include the following:

Name A man page begins with a statement of the command, call, or file that’s described, along with a few words of explanation. For instance, the man page for man (section 1) has a “Name” section that reads man - an interface to the on-line reference manuals.

Synopsis The synopsis provides a brief description of how a command is used. This synopsis uses a summary format similar to that used to present synopses in this book, showing optional parameters in square brackets ({}), for instance.

Description The description is an English-language summary of what the command, file, or other element does. The description can vary from a very short summary to something many pages in length.

Options This section summarizes the options outlined in the “Synopsis” section. Typically, each option appears in a list, with a one-paragraph explanation indented just below it.

Files This section lists files that are associated with the man page’s subject. These might be configuration files for a server or other program, related configuration files for a configuration file, or what have you.

See also This section provides pointers to related information in the man system, typically with a section number appended. For instance, less(1) refers to the section 1 man page for less.