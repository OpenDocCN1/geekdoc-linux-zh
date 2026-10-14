
or

```
$ man -k 'logged in'
```

The system displays the following:

```
rusers (1) - Displays a list of users who are logged in to a remote machine
rwho (1) - Shows which users are logged in to hosts on the local network.
who (1) - Identifies users currently logged in
```

Note

The numbers enclosed in parentheses refer to the section numbers of the reference pages. See the man(1) reference page for a discussion of the structure of the reference page files.

After using the apropos or man -k commands, you now know that several commands: rwho, rusers, and who can be used to display the users who are logged into the system. You can then use the man command to get information on using any of these commands.

## Overview of Files and Directories

This chapter provides an introduction to files, file systems, and text editors. A file is a collection of data stored together in the computer. Typical files contain memos, reports, correspondence, programs, or other data. A file system is the useful arrangement of files into directories.

A text editor is a program that lets you create new files and modify existing ones.

After completing this chapter, you will be able to:

- Create files with the vi text editor. These files will be useful for working through the examples later in this book.
- Understand the file system components and concepts.

This knowledge can help you design a file system that is appropriate for the type of information you use and the way you work.

### 2.1 Overview of Text Editors

An editor is a program that lets you create and change files containing text, programs, or other data. An editor does not provide the formatting and printing features of a word processor or publishing software.

With a text editor, you can:

- Create, read, and write files
- Display and search for data
- Add, replace, and remove data
- Move and copy data
- Run operating system commands

Your editing takes place in an edit buffer that you can save or discard.

The vi and ed text editing programs are available on the operating system. Each editor has its own methods of displaying text as well as its own set of subcommands and rules.

For information about vi, read Section 2.2 and Appendix A. For information about ed, see Appendix B.

Your system may contain additional editors; see your system administrator for details.

### 2.2 Creating Sample Files with the vi Text Editor

This section shows how to create three files with the vi text editor.

The goal of this section is to have you create, using a minimal set of commands, files that can be used for working through the examples later in this book. For more information about vi, see Appendix A and the vi(1) reference page.

> Note
> 
> If you are familiar with a different editing program, you can use that program to create the three sample files described in this section. If you already have created three files with an editing program, you can use those files by substituting their names for the file names used in the examples.

When following the steps that are used to create the sample files, only enter the text that is shown in boldface characters. System prompts and output are shown in a different typeface, like this.

To create three sample files, follow these steps:

1. Start the vi program by typing vi and the name of a new file at the shell prompt. Press the Return key.

```
$ vi file1 Return
```

This is a new file, so the system responds by putting your cursor at the top of a screen:

```
~
~
~
~
"file1" [New file]
```

Notice the blank lines on your screen that begin with a tilde (~). These tildes indicate the lines that contain no text. Because you have not entered any text, all lines begin with a tilde.

2. Type the lowercase letter i to specify that you want to insert text to the new file. The system does not display the i that you enter.

Enter the following sample text, pressing the Return key after each line. To correct mistakes before moving to the next line, press the
