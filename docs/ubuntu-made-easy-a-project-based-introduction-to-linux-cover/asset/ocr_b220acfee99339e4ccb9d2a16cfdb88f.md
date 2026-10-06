# Project 2B: Shredding Documents Digitally

Although most people are satisfied with deleting their files when they no longer need them, they may not realize that the deleted file is still retrievable. This may pose little concern when it comes to photos of your summer trip to Maryland or reports you may have written for a class on Thai cooking, but it is a completely different situation if you were been storing account details or other confidential information on your hard disk. Even if the data stays. That is great news if you want to retrieve any files you may have accidentally deleted (or formatted away), but it isn't such good news if your computer gets lost or is thrown away), if you would just decide to delete it away. In preparation for such cases, it might not be a bad idea to do some digital shredding.

# 20B-1: Trying the shred command

Digital shredding in Linux is done with the shred command. Its usage is similar to the rm command you learned to use in Chapter 8, though in terms of removal, shred is much more thorough. To do it away, create a dummy file by going to the File menu of a Nautilus window and selecting New Document > Empty Document. The new document myShredExp.txt this will open edit. Type a couple of sentences in the document—anything will do—save it. The first couple of words you typed should now appear on the icon of the new dummy file you created (as shown in the example of Figure 20-7).

![](bbox=[0.648, 0.473, 0.863, 0.526])

Figure 20-7: Files change their appearance after being shredded.

With your new file and placed in your Home folder to make it easier to follow, open a Terminal window, type shred myShredExp.txt, and press ENTER. If you look in your Home folder, you will notice the difference right away. Your original file is still there, but the text on the icon looks like gibberish (as you can see on the right side of Figure 20-7), which is what your file has become. If you double-click the file, edit will open as it did before, but this time around, it won't be able to read your file and will tell you so (Figure 20-8).

So, now you've got yourself a shredded file in your folder, but it would be hard to get rid of the file rather than just have it sit littering things up, wouldn't it? Of course you could remove the file via the Terminal using the rm command, but it would be easier if shredded files were deleted immediately after being shredded. Frankly, this is easy to do by using the shred command with the -u flag. You can try it on the file you've already shredded by opening a Terminal window, typing shred -u myShredExp.txt, and pressing ENTER. Your file will then be further shredded and deleted.