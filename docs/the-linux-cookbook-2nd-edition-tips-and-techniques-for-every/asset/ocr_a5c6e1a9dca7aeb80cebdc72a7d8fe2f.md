# 10. Editing Text

Editing text is one of the most fundamental activities of computing on Linux-based systems, or most any computer for that matter. We edit text when writing a document, sending email, making a Web page, posting an article for Usenet, programming—and the list goes on.

Most editing of text is done in a text editor, which is an application that generally opens a file containing some text and lets you rearrange, insert, delete and otherwise edit that text. People spend a good deal of their computing time editing text with a text editor application.

In this chapter, I give introductions to the two most popular text editors out there. I also cover other essential or handy ways to edit text without an editor, including concatenation, file inclusion, and cutting and pasting with the mouse.

There are a lot of text editors to choose from, but everyone knows there are really only two choices: Emacs and Vi. The majority of editors are found under one of these two main branches; more programs may have been influenced by Emacs than by any other application, and almost every UNIX system in the world has some version of Vi installed. Most users prefer one or the other; rarely is one adept at both. Many tools and applications have special modes in which the keystroke commands of Emacs and Vi are recognized, including the Bash shell (see Chapter 3 [The Shell], page 53).

Sections in this chapter are devoted to both. Newcomers, you'll do well to spend a half-hour with each of these editors, setting aside time to try the built-in tutorials. Then, go with the one that resonates.

Emacs and Vi are not like the kind of program you are likely to be familiar with, and some newcomers might seem baffled at first—but they're really not difficult to use, and the experience pays off greatly. Anyone who has experience with either of them knows that one can do much more, and more quickly, in such an editor than with any "word processors" that are out there on other systems. If you run the tutorial for both Emacs and Vi, you can get a feel for how they work, and see which might be good for you (the ways to run them are explained in Recipe 10.1.2 [Running an Emacs Tutorial], page 237 and Recipe 10.2.2 [Running a Vi Tutorial], page 247).

Of course, there are other editors, and many have their devout followers; it is worth having a look at what is available. If you are accustomed to some particular editor on some other system, the chances are great that a "clone" of it exists for Linux. For example, there are editors that work similarly to the EDIT program in DOS, or the old WordStar word processor (there is a special