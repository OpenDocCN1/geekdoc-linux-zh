
GNU emacs. To see whether you have this version, type emacs or gnumacs at the command line.

Still can’t find emacs on your system? Check with your system administrator or do a Google search for the name of your particular OS and the word emacs and see what you can find out. At worst, you can go to the GNU Project site and download a copy: http://www.gnu.org/software/emacs/.

+   2. Rather than start with a blank screen, quit the program (C-x C-c) and restart emacs with one of the earlier test files, dickens.note:

Click here to view code image

```
% gnumacs dickens.note
A Tale of Two Cities          Preface
When I was acting, with my children and friends, in Mr Wilkie Collins’s drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire was upon me then, to embody it in my own person; and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with particular care and interest.
As the idea became familiar to me, it gradually shaped itself into its present form. Throughout its execution, it has had complete possession of me; I have so far verified what is done and suffered in these pages, as that I have certainly done and suffered it all myself.
Whenever any reference (however slight) is made here to the condition of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add --Emacs: dickens.note      (Fundamental)--Top-----
```

As you can see, it’s quite different from the display shown when vi starts up. The status line at the bottom of the display offers useful information as you edit the file at different points, and it also reminds you at all times of the name of the file, which can be surprisingly helpful. emacs can work with different kinds of files, and here you see by the word Fundamental in the status line that emacs is prepared for a regular text file. If you’re programming, emacs can offer special features customized for your particular language.

+   3. Quit emacs by using the C-x C-c sequence but let a few seconds pass after you press C-x to watch what happens. When I press C-x, the bottom of the screen suddenly changes to this:

Click here to view code image

```
on the faith of the most trustworthy witnesses. It has been one of my hopes to add --Emacs: dickens.note      (Fundamental)--Top----- C-x-
```

## Note

Confusingly, the cursor remains at the top of the file, but emacs reminds me that I’ve pressed C-x and that I need to enter a second command after I’ve decided what to do. I now press C-c and immediately exit emacs.

Already you can see some dramatic differences between emacs and vi. If you’re comfortable with multiple key sequences such as C-x C-c to quit, I think you’re going to enjoy learning emacs. If not, stick with it anyway. Even if you never use emacs after trying the examples in this lesson, it’s still good to know a little bit about it.

## Note

Why learn about a tool you’re not going to use? Because as you go from system to system, you never really know what graphical interface, what window manager, and even what editor packages might be available. Being competent at emacs or vi means that even in a worst-case scenario with a very rustic install, you can edit files and proceed with your project. So the answer really is that it’s smart to learn because it’s smart to have options.

## Task 12.2: Moving Around in a File

Files are composed of characters, words, lines, sentences, and paragraphs, and emacs has commands to help you move about among them. Most systems have the arrow keys enabled, which helps you avoid worrying about some of the key sequences, but it’s best to know them all anyway.

The most basic motions are C-f and C-b, which are used to move the cursor forward and backward one character, respectively. Switch those to the Meta command equivalents, and the cursor will move by words: M-f moves the cursor forward a word, and M-b moves it back a word. Pressing C-n moves the cursor to the next line, C-p to the previous line, C-a to the beginning of the line, and C-e to the end of the line. (The vi equivalents for all of these are l, h, w, and b for moving forward and backward a character or word; j and k for moving up or down a line; and 0 or $ to move to the beginning or end of the current line. Which makes more sense to you?)

To move forward a sentence, you can use M-e, which actually moves the cursor to the end of the sentence. Pressing M-a moves it to the beginning of a sentence. Notice the parallels between Control and Meta commands: C-a moves the cursor to the beginning of the line, and M-a moves it to the beginning of the sentence.
