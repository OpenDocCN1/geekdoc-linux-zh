
## Comments About Comments

A comment in a program is text intended strictly for human consumption. The compiler ignores any comments it finds in source code and header files.

Use comments liberally to document your program's source code, credit the program's authors, keep a history of modifications, and for other notes. For instance, I usually keep a list of unfinished business in a comment at the beginning of my program files. This helps jog my memory about what needs doing, especially when I haven't looked at the file recently.

The following sections explain how to write comments using two different styles—one for C and C++ programs, and one for C++ only.

### C-Style Comments

You may use C-style comments in C and C++ programs. This type of comment begins with the double-character symbol /* and ends with its mirror image, */. The compiler ignores both symbols and all text in between, even if that text stretches for two or more lines. For example, this single-line comment might appear at the beginning of a source code file:

```
/* Fishing Database System: by Grouper Tom */
```

Note
Any relation to Grouper Tom and the author is strictly wishful thinking.

You may also write C-style comments on multiple lines. Even so, you need only one set of comment delimiters. For example, you might create a file with commented text that you can insert into new source code files:

```
/* Program name: */
/* Author: */
/* Purpose: */
```

Rather than type all those comment delimiters, you can more easily write those lines this way:

```
/*
Program name:
Author:
Purpose:
*/
```

That looks a little strange; so many programmers pretty things up with some fancy footwork, writing the preceding comment as

```
/*
* Program name:
* Author:
* Purpose:
*/
```

For some reason, this style confuses many programmers when they first see it. But look—there's a starting comment delimiter /* on the first line and an ending delimiter */ on the last. The compiler ignores all the text in between, including the three asterisks in the middle, there only for the sake of neatness. For a fancier effect, many programmers box their comments using text such as this:

```
/* =========================
 * Program name:
 * Author:
 * Purpose:
 * ========================= */
```

That's still just one comment to the compiler. The comment generates no code, and it produces no effect in the compiled program. Even so, it's amazing how much time programmers spend getting their comment file headers just right!

C-style comments don't have to appear on their own lines. They can appear ahead of or even in the middle of statements and other declarations. However, the most common use for comments is to document a statement such as this:

```
cout << "Press Enter...";  /* Tell user to press the Enter key */
```

In this case, the statement's purpose is fairly obvious, and it probably doesn't need commenting, but too many comments are better than too few. Don't hesitate to use comments to document even the obvious statements and declarations in your code.

Comments usually document what the program does, but you can also use them for commenting-out portions of source code that you don't want to erase completely, perhaps because you are chasing down a bug. Examine this statement:

```
cout << "One " /*<< endl*/ << "Two" << endl;
```

Because of the comment delimiters, the compiler "sees" that statement as though written:

```
cout << "One " << "Two" << endl;
```

Compiling and running that statement writes the text "One Two" on a single line. Removing the comments and changing the statement to the following inserts an endl object between the two strings, thus writing them on separate lines:

```
cout << "One " << endl << "Two" << endl;
```

Using C comments as demonstrated here is a simple, but vital, technique to learn. You will frequently comment-out unfinished sections of code or statements that you've copied to try out variations or optimizations. To restore the original code, simply delete the comment delimiters.

### C++-Style Comments

C++ adds to C another kind of comment delimiter that works a little differently. In a C++ program, a double slash // begins a comment. The compiler ignores every character from // to the end of the line. To use a C++-style comment, type // followed by the comment's text:
