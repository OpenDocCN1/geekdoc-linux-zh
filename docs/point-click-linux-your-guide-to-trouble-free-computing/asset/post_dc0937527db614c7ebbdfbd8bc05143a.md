
where you want to delete everything *after* that point and hit “Delete.” All three methods work.

To undo, you go to the top of the KWrite window, click on “Edit,” and click “Undo” — which is handily the top choice. If you want to save half a second, hold the “Ctrl” key while you press the letter “Z.” This does the same thing.

### Keyboard Shortcuts

Most Linux programs have lots of keyboard shortcuts you can use to replace the menu pointing. We’ll cover many of them, but leave you to discover some of the less-common ones for yourself.

Anyway, we have now created text, copied it, and deleted a few words — then undeleted them. These are the basic things we do with a basic text editor. We have two main functions left to explore: “Print” and “Save.”

Printing is dirt-simple: Click on the little picture of the printer in the top of the window, at the right side of the line of icons we call the “toolbar.” If you have your printer set up the way we showed you earlier, your text will print. It won’t have any fancy formatting but will look just like a typewritten page, because that’s all a basic text editor is supposed to do.

“Save” takes a bit more work, but not a lot. The big questions are, “Where do you want to save your note?” and, “What name will you give it?”

This is where we apply what we learned about the file system. If this note is a draft you might want to work on later, perhaps you’ll want to save it on your Desktop so it’ll catch your eye later. If it’s a “Tropical Drink Recipe” (and you made that folder), that’s obviously where it belongs, and the title should be the name of the drink, like “Purple Mimosa.”

The two main rules about saving files:

- Save them in a pattern that makes sense to *you* — and maintain that pattern so you don’t need to fumble around looking for them.
- Use file names that make sense to *you* so you remember what was in them when you see them three months later.

(Note the *you* in there. It’s *your* personal computer. Unless you’re using it at work, and your company tells you how to file different types of information, you choose the way *you* like best, not the way someone else likes it.)

To save your document the first time, click either the little floppy disk picture in the toolbar or the floppy disk picture next to it that has a pencil on it. Either way will bring up a dialog box that asks you where you want to save your work and what you want to call it.

![](img/01efe5dd076565746bf3678068ba155c_47_0.png)

Because this is a “document” you may want to put it in your “Home” top-level folder or in a folder you have created. Or perhaps you will choose to put it on your Desktop. Either way, click on the appropriate folder, then type your name for this folder in the form called “Location” (which has that name because you’re deciding the “file location” where this piece of work will be stored). Then click “Save” and you’re saved.

After you’ve saved this little bit of text once, to save subsequent modifications you make to it, just click the floppy disk icon and the update will save automatically—or type “Ctrl+S” (shorthand for “Hold down the “Ctrl” key and press the “S” key) and you’ll get the same results. You can also click on the “Edit” choice in the program’s top menu, and you’ll see “Save” and “Save As” choices there.

The only reason to use “Save As” on a piece of work you have already saved is if you want to resave it under a different title (location) or in a different format. We’ll talk more about saving in different formats when we start talking about full-fledged word processing with OpenOffice.org and items we create with other programs more complicated than KWrite, which only saves your work as raw text. Yes, if you poke around in the menus you’ll see an “Export” choice that leads to “HTML.” But all you get when you do that is the HTML “pre” command that makes your text look, on the Web, just as if it came from a typewriter, not “real” HTML, which we can (and will) create with other programs later.

## Configuring KWrite

Although KWrite obviously works without any configuration, this is a good time to spend a minute configuring Linux software. In our “Beyond the Basics” section we’ll show you how to customize your software and, indeed, your entire desktop. This is just a taste here, and because we're running from a CD instead of from a hard drive, any changes we make now will be lost when we turn our computer off, so there's no way you can harm anything by experimenting.

We configure KWrite (and other KDE programs) by clicking on “Settings,” then choosing “Configure Editor” from the list of choices.

![](img/01efe5dd076565746bf3678068ba155c_48_0.png)

This brings up a window that gives us choices.

It's easier and faster for you to experiment with those choices than to describe them, so we'll leave you to play with them on your own, but don't feel you're being abandoned without anyone to hold your hand while you experiment. In the lower left corner of that configuration screen you'll see a “Help” button. Click on it, and you'll see a complete manual for KWrite.

Another way to access that manual from the main program is to click on the “Help” menu item at the top of your KWrite window. Almost every KDE program—indeed, almost every Linux program—has a similar manual built-in, accessed through a “Help” button. Some of these built-in “Help” files are great, and some of them are not. (KWrite's Help happens to be one of the good ones.)

Most “Help” files have a way to contact the program's developers directly with bug reports, and those bug reports are invariably read and almost always acted upon. Bugs in KDE are usually fixed far faster than commercial software companies fix *their* bugs. (This is part of the “Magic of Open Source” we'll talk about at the end of the book, after we get you up to speed using Linux, which is our primary goal right now.)

This is enough about KWrite. We'll work with more commands—and extend our knowledge of Linux as we learn how to use other programs—after we get MEPIS Linux installed on our hard drive.

# Chapter 4

# Installing MEPIS Linux on Your Hard Drive

![](img/01efe5dd076565746bf3678068ba155c_50_0.png)

The great thing about a "Live CD" operating system like MEPIS Linux is that we've gotten a little experience with it before taking the step of actually installing it. We know where to get help and answers to questions (www.mepis.org and www.mepis.org/forum), and we have an idea of what software will be installed along with the basic operating system.

Note that we’re not just installing an operating system, but all the software we need to perform basic computing tasks, plus enough games to divert us when we get bored with work—and we’re also installing utilities like a junk email filter, popup blocker, and a firewall so that our computer is safe and secure when we connect to the Internet.

Now comes the big decision: If we already have Windows on our computer, do we want to keep it there, next to our new Linux installation? It is far easier to do a pure Linux install than to set up our computer as a “dual boot” machine, but let’s grip our teeth and start by learning how to install MEPIS Linux while leaving Windows on our system.

> Note: This only works if you have at least a 10GB hard drive. If you have a lot of pictures, music, and other files that take up large amounts of hard drive space, you probably shouldn’t try to have both Windows and Linux on your hard drive unless it can hold 20GB or more. At this point, if you have doubts about your hard drive’s capacity, you may want to consider a total conversion to Linux instead of going the dual-boot route. (Failing that, you may consider adding a second hard drive to your computer or replacing your current hard drive with a bigger one.)

### Setting Up a Dual-boot Linux/Windows System

You can skip these next few pages if you’re ready to work with Linux full-time. But if you are going to keep Windows on your computer along with Linux, you must follow the following instructions very *carefully* or you may end up unable to run either operating system without reinstalling one or the other.

The first two things you must do have to do with Windows, not Linux:

- Back up any critical data.
- Defragment your hard drive. (This is a Windows utility; Windows manuals will tell you how to do this.)

Now it’s time to embark on the adventure of hard drive repartitioning. To do this, open the MEPIS Installation Center by clicking on the appropriate desktop icon.

![](img/01efe5dd076565746bf3678068ba155c_51_0.png)
