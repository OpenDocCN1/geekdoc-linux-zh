# Exiting NASM-IDE

There is more than one way to get out of NASM-IDE once you've finished with the job at hand. The File menu has an Exit item, and that's the easiest to remember, and it will do the job. The shortcut for the File | Exit menu item is Alt-X:

Alt-X exits to DOS.

NASM-IDE keeps track of whether a file has been changed since the last time it was saved to disk. If you attempt to exit NASMIDE with unsaved changes on deck, NASM-IDE will bring up a dialog asking if you want to save your changes. Most of the time you do—and in most cases you'll click the Yes button. But other occasions might arise the best thing to do is abandon a changed file and start again. The most common example of this is a careless Replace all command that went through your entire file and did a lot of unintended and difficult-to-reverse things. The best thing to do in such a case is leave NASM-IDE without saving the damaged file, and then coming back with the most recent copy. This is another good reason to save often: You don't want to abandon a bad “Replace all” change (what some programmers have come to call a “search and destroy”) along with two hours' worth of useful work. Save often. And know when not to save. It's all part of the game.

# Changing the Display Size

By default, NASM-IDE brings up a traditional 25-line by 80-character DOS text screen. This isn't a lot of room to move, especially when virtually every modern display adapter is capable of showing you either 43 lines (on some ancient hardware) or 50 lines on a text screen. When I use NASM-IDE in my own work I use 50 lines, every time.

Setting it is easy. Pull down the Options | Environment menu item. The dialog box shown in Figure 5.9 will appear. The top pane governs your screen size. The default is 25 lines, but you can check 43/50 instead by clicking on the 43/50 lines button. Then when you click on OK, the screen size will change immediately.

What it changes to depends on your hardware. If you have an EGA (Enhanced Graphics Adapter) (which is most unlikely in the year 2000),