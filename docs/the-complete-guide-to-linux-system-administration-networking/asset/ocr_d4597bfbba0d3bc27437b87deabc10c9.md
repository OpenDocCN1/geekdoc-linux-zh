You can enter :h to view the vi help file. Within the help file, you can find references (which are actually hyperlinks) to other help files. When the cursor is on one of these references, you can press Ctrl+] to jump to that file. Press Ctrl+T to return back to your previous place (like pressing the Back button in your Web browser). When viewing the help file, enter :q to exit and return to working on your own file.

To search forward from your current cursor position, press the forward slash while in command mode. The slash appears on the bottom line. Enter the pattern you want to search for, then press Enter. You can use a regular expression as the search pattern; the position indicators that tie a pattern to the beginning or ending of a line are useful when searching in vi. For example, to search for the word "configuration" occurring at the beginning of a line, starting with either lowercase or capital "C", you press / then type ^[cC]onfiguration] and press Enter. You are then moved to the first occurrence that matches the regular expression you entered; other matches are highlighted on the screen.

To move to the next matching occurrence of a pattern you entered, press the n key (in command mode).

You can also search backward from the current cursor position by pressing ? in command mode instead of / before entering the search pattern. Whether you use / or ? to enter the search pattern, you can also press N to search backward for other occurrences of the pattern (without reentering the regular expression).

More complex than just searching for a pattern are the search-and-replace operations you can perform in vi. These are initiated using a colon (:) and take the following general form:

```
:line-number-range s/search-pattern/replacement text/flags
```

Although this is a bit more complicated than your average word processor, it's also a lot more powerful and flexible (and usually a lot faster).

The line number range lets you perform this task (or many others you will learn about as you study vi) only on a part of a file. Because it's normal to perform an operation on an entire file, however, you often use the range 1,$, which means "from line 1 to the last line of the file." The s/ / combination indicates a search-and-replace operation. Though it may not seem intuitive, you will at least find it familiar—you'll see the same technique used in other programs later in this chapter, as well as other situations you might encounter, such as the Perl programming language. Perl is a programming language that developers use to create scripts for working on text files and completing other complex tasks.

The only flag you should know immediately is the g flag, for global. Without this flag, the replacement only occurs once per line. With the g flag, all instances in the range you indicate are affected.