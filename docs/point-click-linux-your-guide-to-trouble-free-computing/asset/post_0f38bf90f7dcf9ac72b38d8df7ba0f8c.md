
## 18: gFTP—An Easy, Powerful FTP Program

  To download (or upload) a file, highlight it with your left mouse button, make sure you're in the correct directory on the computer to which you want to transfer it, and press the appropriate arrow button. Then, if it's a big file that's going to take a long time to transfer, go do something else. gFTP will work fine without you watching. Your gFTP screen will look something like this while the file transfer is in progress:

![](img/01efe5dd076565746bf3678068ba155c_154_0.png)

### Working with a Remote Server

  Log in exactly the same way as in any other FTP client. You can see the form spaces for server name, user name, and password in the screenshots. Use them appropriately. You can also add the FTP site you're on as a bookmark so you don't need to enter that information again. Check the "Remember Password" box and even your password will be remembered. Quite a time-saver!

![](img/01efe5dd076565746bf3678068ba155c_154_1.png)

  You can either type in remote server directories as filenames in the space above the "file listing" window on the right half of your gFTP screen or navigate the remote server's file system by clicking on directories, folders, and files. After you found the file or directory you want to transfer or modify, highlight it by clicking on it. To modify that file's permissions and characteristics (assuming you have permission to do this on that remote server, right-click on it and choose from the list of commands that will pop up. All your old favorites are there.

### Point & Click Linux!

  Because Linux is similar to Unix, and all FTP file commands are Unix-based, you can make all the same changes on your local files with gFTP, too. This is usually pointless because you have an efficient, built-in file browser that makes file management on your computer easier than doing it through an FTP program. However, it’s a cute little trick you can use if, for instance, you spot a typo in a file name while working with FTP and want to change it before you forget.

![](img/01efe5dd076565746bf3678068ba155c_155_0.png)

### The gFTP Toolbar

  The icon button on the left is what you click to make a connection after you have the correct information (server name, user name, and so on) typed in. Over to the right, the little button that says “FTP” allows you to switch protocols; you can use gFTP for HTTP transfers and—more useful—for secure transfers with SSH (Secure Shell protocol).

  The rest of the toolbar functions are self-explanatory. Click on the text menu items at the top of the gFTP window and you’ll instantly see what functions are available though each one. Only the “Help” button is disappointing; there is no built-in manual for gFTP. On the other hand, you could argue that there is no need for one since gFTP is so simple, obvious, and stable.

  gFTP help and information is available at www.gftp.org.

## Chapter 19
## K3b—Easy CD Burning Program

  We chose K3b as the CD and DVD burning program to include in the SimplyMEPIS CD and this book because it is one of the finest and most versatile programs of this type we have ever used, in any operating system. K3b handles music, video, and data equally well, and has no trouble burning the “ISO” (complete file system image) CDs needed to boot your computer directly from its CD drive. This is the program that was used to create the original master version of the SimplyMEPIS bootable CD and the video instruction DVD included with this book.

  You can also use K3b to copy almost any kind of CD or DVD that doesn’t have some sort of built-in copy protection, although you will want to make sure you don’t make illegal copies of movies or songs that are protected by copyright laws where you live.

  Remember, too, that if your drive won't burn DVDs, no software—not even K3b—can make it into a DVD-burner. Most RW (Read/Write) drives that can *read* DVDs can't *make* them, even if they do a fine job of writing CDs.

### Running K3b

  So far we haven't encountered a CD or DVD drive that K3b failed to detect or that needed any setup action beyond clicking “Okay” on the defaults. When you start K3b for the first time it will detect your CD RW (or DVD RW) drive and that will be that. You will soon be taken to an opening screen that has a big “Tooltip” window splashed across it.

  As with all other Linux programs, you can keep the “Tips” windows from showing up when you start the program by unchecking the “Show tips on startup” box. It's probably a good idea to let them come up at least the first few times you open the program—and to actually read them, because they contain useful information. Or you may want to click “Next” on the K3b tooltip window four or five times and read all the tips at one time, then shut them off for the future. (K3b is so easy to use that there aren't a lot of tips, so this might be best.)

![](img/01efe5dd076565746bf3678068ba155c_157_0.png)

  Now we have K3b set up (automatically) and ready to run. So let's do something with it. The main startup screen gives us several choices. We're going to choose "New Data CD Project" because we often create Data CDs. In this case, the data will be a bunch of pictures we took of a sailboat race. We're going to make a CD with all the pictures on it that we can give to the editor of the Sarasota Sailing Squadron's monthly newsletter, "The Burgee," for publication in the next edition.

![](img/01efe5dd076565746bf3678068ba155c_158_0.png)

  We have four types of projects from which to choose:

1. New Audio CD Project
2. New Data CD Project
3. New Data DVD Project
4. Copy CD

![](img/01efe5dd076565746bf3678068ba155c_158_1.png)

  K3b considers everything other than music "Data," and we're writing to a CD, so we'll choose "New Data CD Project."

  After we make that choice, we need to choose the data we want to put on the CD. The top half of our K3b screen is divided into two sections: files on the right, folders on the left. We're going to put an entire "Pictures" folder on CD, so we put our cursor on the "Pictures" directory listing and, while holding our left mouse button, drag it down into the "Current Projects" area, then release the mouse button.

![](img/01efe5dd076565746bf3678068ba155c_158_2.png)

  We look down in the lower left corner of the window and see that we have 69.4 megabytes of data in our "Pictures" folder, which will easily fit on a single CD. There's only one thing left to do, assuming we've put either a blank recordable CD or a rewritable CD in our drive: Click the "Burn" button in the lower right corner of the K3b window and sit back.

![](img/01efe5dd076565746bf3678068ba155c_159_0.png)

  Making a music CD is exactly the same, except you choose "Audio CD Project," and instead of selecting a whole folder at once to put on the CD, you might want to place each file (that is, each piece of music) individually on it so you can set the order in which they'll play on the finished CD. To move files around within the "Project" listing, you just "drag" them to where you want them with the mouse while holding the left mouse button and release the button where you decide they best fit in your custom-made playlist.

### More About Using K3b

  When using Reusable (Rewritable) CDs, K3b will automatically "blank" them—that is, remove what you had on them before—but will ask you to confirm this action first so you don't delete important material by mistake.

  Copying CDs is self-explanatory; just step through the processes as they come up, following the onscreen instructions.

  Making or copying DVDs is the same as working with CDs, except you must have a DVD burner and not just a CD burner to use this feature.

  Burning ISO images from which your computer can boot directly (like the SimplyMEPIS CD in this book) requires a slightly different procedure. Select "Tools," then "CD," then "Burn CD Image." (Or if you have a DVD-write drive, you can burn a bootable DVD instead by clicking "DVD" instead of "CD." After that, select the ISO image you want to put on CD or DVD, and you will get a special screen for ISO burning.)
