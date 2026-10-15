# Saving in vi

You’ll want to save changes to your documents frequently, especially as you’re learning to use vi (Figure 4.12). Until you’re accustomed to switching between command and input mode, you may accidentally type in commands when you think you’re typing text, with unpredictable results. To save files, just follow these steps.

# To save text in vi:

+   - Esc :w limerick

Press Esc to get out of input mode and into command mode, then type :w (for "write," as in write to the disk) followed by a space and then the filename (limerick in this example) you want to use for the file, then press Enter. If you’ve already saved the file once, just press Esc and type :w then press Enter.

# Tips

+   - If you’ve already saved your file at least once, you can save changes and exit vi in one fell swoop. In command mode, type :wq (for "write quit"). For more information about quitting vi, see the section called Exiting vi later in this chapter.

+   - If you want to save a file over an existing file (obliterating the original as you do), use :w! existingfilename in command mode. The ! forces vi to overwrite the original.

![](bbox=[0.62, 0.11, 0.92, 0.38])