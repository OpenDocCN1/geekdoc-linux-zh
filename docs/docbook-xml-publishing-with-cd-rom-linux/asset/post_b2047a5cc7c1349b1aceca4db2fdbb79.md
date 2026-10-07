
# Getting Emacs

Emacs - Fast, Speedy, contact@example.org

# How to Files Edit Search Make Help

Welcome to Emacs, a component of a GNU-based system.

- C-h Could hold down and press h
- C-x Changes Last files
- C-u Insertion Use tools to read docs
- C-g ESC or ESC

M-x uses the Meta key; M means the Meta (Alt) key.
If you have no Meta key, you may use type C-C followed by the character

Emacs 25.2.2 *built for you, a toolkit*
Free version 25.2.2
Copyright (C) 1984-present Free Software Foundation, Inc.

Emacs comes with NO WARRANTY; type C-h GNU for full details.
Free Software is free in freedom so you can redistribute copies
and modify it; type C-h LIC to see the conditions.
type -h for information on getting the latest version.

```
C-x Internet --lf-ALT
```

![](img/81f56bf497dbf7f7582072400d12cb42_194_0.png)

console, without the mouse support, type emacs -nw in any terminal that you want. Emacs, you are presented with the Emacs welcome screen. Next you will practice getting around in Emacs by creating a new file.

To create a new file, Emacs type C-x C-f. at the bottom of Emacs to save a file, type C-x C-s, which means Emacs find files: ~/ to open a file in your home directory. However, because you want to create a new file, type the name of the file with which you want to work.

Emacs is a multiplatform program, it takes heavy influence from the Unix environment. The character ~, or tilde, is shorthand in UNIX for your's home directory. For instance, if you want to indicate the path to a home directory, you type ~/path/to/file.txt instead of /home/zonker/path/to/file.txt and the shell interprets the

![](img/81f56bf497dbf7f7582072400d12cb42_194_1.png)

# Chapter 8: Using Emacs

![](img/81f56bf497dbf7f7582072400d12cb42_195_0.png)

Figure 8.8 Creating a new file with Emacs

Now that you have a new file to play with, you can start working. First, though, let me explain how to bail out of a mistyped command. Emacs has many commands, and they can be confusing. Sometimes you might type the wrong command, or you might just have had 10 thumbs like me. When you type C-x C-f (open or create file) instead of C-x C-s (save file), you must press Escape three times to bail out—that's ESC ESC ESC—and Emacs will return to normal operation.

Type a few lines in Emacs so that you have something to play with. Try the traditional "The quick brown fox jumped over the lazy dog" (see Figure 8.9).

# Moving around in Emacs

Now that you are at the end of the sentence, move backwards a bit. You can move around in Emacs the traditional way—with the arrow keys at a console or with the mouse in a GUI environment—or you can get around even faster. Table 8.1 presents Emacs movement key bindings.

![](img/81f56bf497dbf7f7582072400d12cb42_196_0.png)

Figure 8.9 Getting used to Emacs

# Table 8.1 Emacs Movement Key Bindings

| Movement Commands | Action |
|--- |--- |
| C-v or the Page Up key | Forward one page |
| ESC-v or the Page Down key | Back one page |
| ESC < or the Home key | Beginning of the file |
| ESC > or the End key | End of the file |
| C-f | Forward one character |
| C-b | Back one character |
| C-p | Preceding line |
| C-n | Next line |
| C-a | Beginning of the line |
| C-e | End of the line |
| ESC-f | Forward one word |
| ESC-b | Back one word |

Try moving around in Emacs using the hot-key combinations instead of mouse or arrow keys. It might take a day or two to get used to, but when you do, it's very easy. You will be able to zoom around your documents like never before. Note that you need to use the Shift key as well to get the > and < characters.

Why, oh why, are there so many darned hot keys in Emacs and vi, you might ask yourself. Well, there is a very good reason. Both Emacs and vi were designed in days when mice were practically unheard of and most work was done on terminals by programmers, not average humans like you and me. Remember, the guys who invented Emacs and vi were from the old school, still using punch cards to enter data into computers. Hot keys were practically heaven compared to.

Actually, Emacs and vi aren't so old. WordPerfect users can probably remember most of the hot keys from MS-DOS versions of WordPerfect. In fact, nearly all modern applications respect F7 as the key to initialize spell check (There are probably others, but spell check is the one I remember...). Even today, in the world of ultra-slick word processors such as Microsoft Word and publishing programs such as Quark, hot keys abound. You don't need to learn the hot keys to use Word, it's true. If you care to, though, you can use Word seldom ever touching the mouse, depending on what you're doing. The bottom line for writing is that even memorizing the hot keys might seem like a huge hurdle at first, you will see your productivity soar.

![](img/81f56bf497dbf7f7582072400d12cb42_197_0.png)

# Searching and Replacing in Emacs

To move around even faster, try using search functions of Emacs to move around the file. If you're in a lengthy document, even moving one page at a time can be slow. However, if you know that you're looking for the sentence with it you can use search function to jump straight there. Table 8.2 shows a list of search bindings.

# Table 8.2 Emacs Search key bindings

| C-Commands | Action |
|---|---|
| C-s | Search forward. |
| C-r | Search backward. |
| C-s C-s | Repeat last forward search. |
| C-s C-r | Repeat last backward search. |
| ESC | Search and replace. |
| RETURN | End search. |

In search and replace operations, Emacs asks for the string to search for and the replacement text, (see Figure 8.10). By default, Emacs asks before replacing text. To approve the change, type y or press Space. If you don't want to replace the text, type n or press Delete. When you're done searching and replacing, type RETURN and you will return to normal editing mode.

![](img/81f56bf497dbf7f7582072400d12cb42_198_0.png)

Figure 8.10 Search and replace with Emacs

# Cutting and Pasting in Emacs

The cut and paste functions in Emacs are straightforward. Type C-d to delete the character the cursor is currently on and DEL to delete backwards. To make life easy, or at least easier, Table 8.3 shows the key bindings for cutting and pasting in Emacs.

![](img/81f56bf497dbf7f7582072400d12cb42_199_0.png)

Depending on your key mapping, the Backspace key and Delete key may not do the same thing. You might have to get used to using the Delete key instead of Backspace key, depending on how Emacs reads your map. This is a throwback to keyboards with only a Delete key.

# Table 8.3 Cutting and Pasting

| Command | Action |
|---|---|
| C-d | Delete current character. |
| DEL | Delete preceding character. |
| ESC DEL | Delete the preceding word. |
| ESC d | Delete the next word. |
| C-y | Restore deleted text (paste). |
| C-w | Delete highlighted/marked text. |
| C-k | Delete to end of line. |
| C-x u | Undo the last edit. |

As you can see, Emacs has a plethora of options for manipulating moving around. It might take a little while to get used to, but when you have the hang of Emacs, you probably won't want to work in a regular word processor again.

# Accessing Menus

If you're using Emacs at the console or if you want to get around without the mouse, you can access the Emacs menus by using the hot-key combination ESC `, which opens a split window with the menu choices (see Figure 8.11).

# Help!

You want to find out more about Emacs, Emacs' online help function to set a tutorial, type C-h t Emacs will take you into your tutorial mode. To get information about a key combination, type C-h k, which will give you a prompt to type the key combination about which you need more information. Figure 8.12 shows Emacs' help function in action. You can also access the Help menu from the keyboard, although, some choices under the Help menu not related to help at all, such as the Cursor menu.

Emacs being the lovable customizable behemoth that it allows, for various editing modes. One of the major modes for Emacs is the PSGML mode, a finite mode-based model built with Emacs Lisp. This is an extensible model built with sum in Emacs. Best of all major modes respond ending and unmodified for all types systems were seen programming languages As base Emacs modes which are built and run in Emacs Lisp.
