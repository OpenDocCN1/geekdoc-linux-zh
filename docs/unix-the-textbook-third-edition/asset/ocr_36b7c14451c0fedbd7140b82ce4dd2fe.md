Step 5: Expand the highlighted area by using the input device of your choice until all the text you typed in Step 2 is highlighted. If you make a mistake in defining the block, use <Esc> to stop the block definition and begin highlighting again at the first character in the buffer until you get the block definition you desire.

Step 6: Type y.

Step 7: On the last line display you will see a report of how many lines you just yanked.

Step 8: Position the cursor anywhere on the last line of the buffer.

Step 9: Type o. A new line opens below the last line in the buffer. Press <Esc>.

Step 10: Type p. The yanked block from Step 6 is put back in the buffer, starting on the new line you opened in Step 9 and proceeding downward. Save the file if you want to.

# 3.2.6.3 Using Gvim to Cut and Paste between Multiple Open Buffers

To illustrate the speed and efficiency of using gvim as a modern graphical UNIX text editor, and to describe some of gvim's functions, the following practice session allows you use gvim to create text in two different files, open buffers into those files in two different windows, and copy and paste between those buffers.

In general, all of the vi commands and operating modes shown previously work in both vim and gvim.

# 3.2.6.4 Practice Session 3.5

Step 1: At the shell prompt, type gvim gvim1 and then press the <Enter> key.

Step 2: Type A and then type This is the first line of text. Then press the <Enter> key twice.

Step 3: Type This is the third line of text. Then press the <Enter> key.

Step 4: From the gvim pull-down menu, make the choice Window>Split. You now are looking into two windows on the same buffer.

Step 5: From the gvim pull-down menu, make the choice File>Save. Click the OK button in the Save window. The buffer is saved to the file gvim1.

Step 6: Use the mouse and click anywhere in the lower window with the left mouse button. You are now working in the lower buffer.

Step 7: From the gvim pull-down menu, make the choice File>Save As. In the Name box, change the name of the file to gvim2, and then make the Save button choice. The buffer is saved as gvim2, and you are looking into the buffer through two windows.

Step 8: The active buffer is still seen in the lower window. Use the mouse and <Delete> key on the keyboard to change the word first to the word second, and the word third to the word fourth in the lower window.