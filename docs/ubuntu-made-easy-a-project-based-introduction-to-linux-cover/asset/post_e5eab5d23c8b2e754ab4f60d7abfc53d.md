
- 3. In the Compress window that appears, type blossoms in the Filename text box and then select .zip from the drop-down menu button to the right of that. Everything looks like what I've set up in Figure 7-22, click the Create button, after which a compressed archive of your two files (blossoms.zip) will appear in your Home folder.

![](img/d35fa962e6f9664d66dc83916f426418_161_0.png)

Figure 7-22: Creating a compressed archive

Now that you know how to put things together, let's learn the simple task of ripping it all apart—well, okay, extracting your files:

- 1. Drag the original dogwood and violet files to the Trash to get them out of the way.
- 2. Double-click the blossoms.zip file you've just created. A window showing the contents of the file will appear (Figure 7-23).

![](img/d35fa962e6f9664d66dc83916f426418_161_1.png)

Figure 7-23: Extracting a compressed archive

- 3. In that window, click the Extract button, after which another window, Extract, will appear.

- 4. Click the Extract button in that window, and within a second (two at most), you will find two new copies of dogwood and violet in your Home folder.

Now you've created and extracted a compressed archive, which is in this case a Zip file. You can also create a compressed tarball in the future following the same procedure (probably with real rather than dummy files), but when it's time to select an archive type, select .tar.gz instead of .zip. Other than that single step, it is the same creation and extraction process.

![](img/d35fa962e6f9664d66dc83916f426418_162_0.png)

# SIMPLE KITTEN WAYS

Getting to Know the Linux Terminal and Command Line . . . and the Cool Things It Can Do

![](img/d35fa962e6f9664d66dc83916f426418_162_1.png)

Many people shy away from Linux because they envision it as a system for computer-geeks, an environment in which you do everything the hard way—by command line. In this era of graphical interfaces, the idea of typing commands to get things done seems like a dreadful throwback to the days of DOS, and that puts many people off, especially those who remember the “old days.”

This reaction is far off, but it is not an accurate reflection of the reality of the Linux world. After all, most Linux today utilize some sort of graphical interface. They can, and often do, achieve all that they hope to achieve through drop-down menus and mouse clicks alike. Many are able to survive quite happily without ever opening their Terminal. The same can be true of.

But as it may, there is still much to be said for the power and convenience of the command line. The fact that the command line can now be utilized within a graphical environment also makes it much less forbidding. The Terminal is just a tiny text-based island in a sea of graphical bodies (see Figure 8-1). Using the command line can be as pain-free as anything else you do on your system, and it can actually provide you with a little fun if you are willing to give it a try.

![](img/d35fa962e6f9664d66dc83916f426418_163_0.png)

Figure 8-1: Putting the Terminal into perspective

Unfortunately, many guides to using the command line are written by hard-core command-line junkies, whose enthusiasm for what they see as a really good thing inadvertently makes what they write even more off-putting to the recent Linux immigrant or wannabe.

For your sake, I will try not to go with enthusiasm so as to scare you right back to Chapter 6 and the more comfortable world of the Ubuntu Software-Center. I will also try to keep things in perspective by teaching you, whenever possible, to use the command line as a complement or alternative to the graphical tools you have at your disposal, rather than presenting it as the sole way of going about things. Of course, I am not going to cover every possible angle in this regard—just enough to give you some exposure and experience and, ideally, make you feel a little more at ease with the command line. Who knows? You might actually come to think of using the command line as . . . fun? Well, I won't get too carried away.

# Meet the Terminal

You can run the Linux command-line Terminal application in your Ubuntu system by going to the Dash, typing terminal, and pressing ENTER. When the Terminal opens, it will, in all its simplicity, look much like Figure 8-2.

```
rg@mydesktop:~
rg@mydesktop:-$ []
```

Figure 8-2: The Terminal application

As you can see, all it says is rg@mydesktop:$. In this case, rg is my username, mydesktop is the name I gave my computer during installation, and the tilde (~) signifies that I am in my Home folder. If it were to say~/Music, for example, it would mean that I am currently in the Music folder within my Home folder. Of course, all this will be different in your case, because your username and computer name are wetrock, for example, the command line will say frog@wetrock:$. If all this sounds rather obtuse to you, just think of it this way: username@computer_name:$ in the Terminal is the equivalent of your Home folder in Nautilus.

- 1. Type I like strawberries so very much.
- 2. Change strawberries to cherries. (You've changed your mind!) Start using your left arrow key to move the cursor in the first s in strawberries.
- 3. Tap your DELETE key as many times as necessary to erase the word strawberries (that would be 12 times, methinks).
- 4. Type cherries and then use your right arrow to move the cursor back to the end of this meaningful sentence.

Now that you've completed this fascinating bit of typing practice, press the ENTER key. As you will almost immediately see, the Terminal's response to your efforts thus is merely a dismissive &: command not found. Although you've typed a string of text that has meaning to you, it means absolutely nothing to your system. In fact, the system was so shortsighted that it could see nothing other than the first word you typed in the Terminal (I), and because I is not a valid command, the system had no idea what to do with it.

Simple Kitten Ways 127

# Some Goofy Useful Fun with the Command Terminal

A rather cool thing about typing in the command Terminal is that you might call short-term memory. Try it by typing the word cherry and pressing ENTER. Ignoring the command-not-found message, go on and type vanilla and press ENTER. Now type gelato and press ENTER. So far, so dumb, right? Well, not really. Let's try everything you typed far again, but this time's left to it with one key.

Huh?

Yes, just press the up arrow key once, and what do you see? That’s—the last command you typed appears, in which case would be gelato. Press the up arrow key again, and the command that you typed before that appear—vanilla. One more time? Yes, cherry. And one more time for the finale ... I like cherries so much.

Considering what we have thus, this may all seem a bit silly, but imagine you're not typing little words and instead have to deal with longer strings, like a simple copy (which you'll learn in this chapter) like this:

```
cp Photos/mypics/stprier/coastal/onbeach_27.jpg /home/frog/photos_for/stprier
```

By typing you are copying an image called onbeach_1.jpg from the coastal folder to another called onbeach_1. If you wanted to copy another photo in the coastal folder, onbeach_16.jpg, for instance, you could simply press the up arrow key once, use the left arrow key and DELETE key to move over and delete the 27, and replace it with 16. All in all, it would be much simpler and much faster. It would also help you avoid mistakes in typing. Not so dumb anymore, eh?

# Nontoxic Commands

As you know all, all of this typing is easy enough, but to actually do something with your Terminal, you need to type commands—and there are more of them than you could ever hope or know. To get started, we will begin with some commands that are easy to understand, nontoxic, and completely kitten friendly.

# $whoami

There is no command as easy, safe, or as seemingly useless as whoami. Rather than help with multiple personality disorders discover who they are at any given moment, the whoami command simply tells you user is currently logged in. Try it by typing whoami the $ and then pressing the ENTER key. Remember that commands are case sensitive.
