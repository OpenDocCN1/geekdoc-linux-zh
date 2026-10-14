
Delete key or the Backspace key to move backward over the mistake. Retype the text correctly.

```
You start the vi program by entering Return
the vi command optionally followed by the name Return
of a new or existing file. Escape
-
-
-
-
"file1" [New file]
```

3. Press the Escape key to indicate that you have finished your current work. Type a colon (:) to enter the Last Line mode.

## Note

Depending upon how your terminal or workstation is set up, the Escape key may be programmed to perform a different function. It is possible that one of the function keys on your keyboard may have been set up to perform the escape function. This function is often assigned to the F11 key. See your system administrator if your Escape key does not operate properly.

The colon is displayed as a prompt at the bottom of the screen as follows:

```
You start the vi program by entering
the vi command optionally followed by the name
of a new or existing file.
-
-
-
-
:
```

4. Enter a lowercase letter w next. Entering the letter w indicates to the system that you want to write, or save, a copy of the new file in your current, user directory (see Chapter 4 for an explanation about your current directory).

Your screen will look like this:

```
You start the vi program by entering
the vi command optionally followed by the name
of a new or existing file.
-
```

```
"file1" [New file] 3 lines, 111 characters
```

The system displays the name of the new file as well as the number of lines and characters it contains.

The system is still in the vi text editor so you can create two more sample files. The process is the same as the one you used to create file1, but the text you enter will be different.

5. Type a colon (:). The colon is displayed as a prompt at the bottom of the screen. To create your second sample file, enter vi file2. The system responds with a screen that looks like this:

```
"file2" No such file or directory
```

The message file2 No such file or directory indicates that file2 is a new file.

6. Indicate that you want to insert text to the new file by typing the lowercase letter i. Enter the following sample text:

```
If you have created a new file, you will find Return
that it is easy to add text. Escape
```

7. Type a colon (:) and enter the lowercase letter w to write, or save, the file in your current directory.

Your screen will look like this:

```
If you have created a new file, you will find
that it is easy to add text.
```

```
"file2" [New file] 2 lines, 75 characters
```

8. Follow the instructions in step 5 to create the third file. However, name the file file3, and enter the following sample text:

```
You will find that vi is a useful Return editor that has many features. Escape
```

9. Type a colon (:) and enter the wq command.

The wq command writes the file, quits (that is, exits) the editor, and returns you to the shell prompt.

## 2.3 Understanding Files, Directories, and Pathnames

A file is a collection of data stored in a computer. A file stored in a computer is like a document stored in a filing cabinet because you can retrieve it, open it, process it, close it, and store it as a unit. Every computer file has a file name that both users and the system use to refer to the file.

A file system is the arrangement of files into a useful pattern. Any time you organize information, you create something like a computer file system. For example, the structure of a manual file system (file cabinets, file drawers, file folders, and documents) resembles the structure of a computer file system. (The software that manages the file storage is also known as the file system, but that usage of the term does not occur in this chapter. On some systems, this software is also called the file manager.)

Once you have organized your file system (manual or computer), you can find a particular piece of information quickly because you understand the structure of the system. To understand the file system, you should first become familiar with the following three concepts:

- Files and file names
- Directories and subdirectories
- Tree structures and pathnames

### 2.3.1 Files and File Names

A file can contain the text of a document, a computer program, records for a general ledger, the numerical or statistical output of a computer program, or other data.

A file name can contain any character except the following because these characters have special meaning to the shell:

- Slash (/)
- Backslash (\)
- Ampersand (&)
- Left- and right-angle brackets (< and >)
- Question mark (?)
