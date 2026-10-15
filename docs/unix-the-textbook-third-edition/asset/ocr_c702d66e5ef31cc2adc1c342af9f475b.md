Figure 3.14 shows warning messages, but not exceptions that prevented compilation and linkage.

Step 6: If all syntax errors have been removed from the power.c source code, you should get a screen display similar to Figure 3.14, which indicates in the bottom buffer window that you have successfully compiled and linked power.c.

Step 7: You can now exit emacs, and in a terminal window test the program by typing power on the command line. Remember that the path must be set for the current shell so that executable programs in the directory the file power is in will run.

# 3.3.12 Working in Multiple Buffers

As seen in previous exercises, it is possible to insert one buffer into another and to open windows into different buffers, some of which may not even contain text you want to edit, at the same time. This capability is important when you want to compose the contents of a buffer or file from perhaps many other buffers or files that you have previously created. The following practice session shows you how to create, move between, and copy and paste between several buffers open within one emacs frame.

# 3.3.12.1 Practice Session 3.14

Step 1: Create a subdirectory under your home directory named multi, and make that subdirectory the current working directory.

Step 2: At the shell prompt, type emacs newfile. You should now be editing the buffer newfile with a single window.

Step 3: In emacs, make the pull-down menu choice File>New Window Below. The frame should now be split horizontally, so that you have two windows, one above the other, both showing the contents of newfile.