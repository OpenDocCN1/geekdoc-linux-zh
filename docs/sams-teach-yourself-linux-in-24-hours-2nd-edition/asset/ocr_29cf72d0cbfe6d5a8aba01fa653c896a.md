# TABLE 4.2 ORGANIZATION OF A MANUAL PAGE

| Section | Description |
|---|---|
| Name | The name of the command and a brief description |
| Synopsis | How to use the command and command-line options |
| Description | An explanation of the program and its options |
| Files | A list of files used by the command and their location |
| See also | A list of related man pages |
| Diagnostics | A description of unusual output |
| Bugs | Known problems |
| Author | The program's main author and other contributors |

Online manual pages contain special typesetting codes for the nroff text formatting program, using special macros (as documented in man.7) that control how the manual page is displayed or printed. For more information on the nroff text formatting program, see Hour 15, "Preparing Documents." The nroff format also is critically important for other programs, such as makwhatis, whatis, and apropos, which you'll learn about later in this chapter. These programs expect manual pages to have a consistent format so that information can be properly displayed during search operations or properly stored when building an information database about your OpenLinux system's programs.

You can also find more detailed documentation for Linux commands and other subjects under the /usr/doc directory, which contains files called Frequently Asked Questions, or FAQs, and How-To documents, or HOWTOs. Additionally, the Free Software Foundation, which releases the GNU software packages, puts much of its documentation in a special hypertext info format. Many of the commands discussed in this book are GNU programs.

![](bbox=[0.08, 0.88, 0.2, 0.96])

Much of the software for Linux comes from the Free Software Foundation, founded by Richard Stallman, author of the emacs editor (see Hour 14, "Text Processing"). The FSF distributes its software under the GNU General Public License, or GPL. Part of the success and popularity of Linux and GNU software is because of the terms of the GPL. If you want more information about the GNU software programs for Linux, the FSF, or the GNU GPL, you can try the info command, which is a reader for the GNU hypertext documentation found under the /usr/info directory. You can also use the man command like so: `man GPL`