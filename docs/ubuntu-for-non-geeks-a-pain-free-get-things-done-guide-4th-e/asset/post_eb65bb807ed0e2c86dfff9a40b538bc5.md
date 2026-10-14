
![](img/f7cef0df22f9dba5a41777808c98eece_388_0.png)

*Figure 19-10: gedit can’t open your shredded files.*

So, now you’ve got yourself a shredded file sitting in your folder, but it sure would be handy to get rid of the file rather than just have it sitting there littering things up, wouldn’t it? Of course, you can remove the file via the Terminal by using the `rm` command, but it would be easier to get future shredded files deleted immediately after being shredded. Fortunately, this is easy enough to do by using the shred command with the `-u` flag. You can try it on the file you’ve already shredded by opening a Terminal window, typing `shred -u myShredEp.txt`, and then pressing ENTER. Your file will then be further shredded and deleted.

## 19C-2: Taking the shred Command Graphical in Nautilus

Although using the shred command isn’t all that difficult, most average users would prefer to do things graphically. After all, you don’t *have* to type commands to delete or move a file, right? You can do all of that easily enough through Nautilus, and it’s the same with shred. The only difference is that shred’s functionality does not come bundled into Nautilus out of the box—you have to add it yourself. Here are the steps you need to follow:

- 1. From the Ubuntu Software Center, search for *nautilus-actions*, and install Nautilus Actions Configuration. This package allows you to add commands and other functionality to Nautilus.
- 2. Once the installation is complete, select **System ▸ Preferences ▸ Nautilus Actions Configuration**.
- 3. When the Nautilus Actions window appears, click the **Add** button.
- 4. In the Add a New Action window that appears, type **Shred** in the Label box and **Erase files more securely** in the Tooltip box.
- 5. If you want to choose an icon for your Shred menu entry in Nautilus, click the arrow button to the left of the Browse button, and then select an icon of your choosing (I just used the delete icon). When you're finished, your window should look like that in Figure 19-11.

![](img/f7cef0df22f9dba5a41777808c98eece_389_0.png)

*Figure 19-11: Making the shred command graphical via Nautilus*

- 6. Next, click the **Command** tab, and type **shred** in the Path box, and **-f -u -v -z %M** in the Parameters box (making sure you use an uppercase M).
- 7. Now click the **Conditions** tab. In the Appears if selection contains section of that tab, choose whether you want the new Shred menu to appear only when you have selected a file, only when you've selected a folder, or both. To play it safe at first, you might want to stick with the default, Only files, so you don't inadvertently shred a whole folder full of important files. Once done, check the **Appears if selection has multiple files or folders** box, and then save your work by going to the **File** menu and selecting **Save**.
- 8. The label for the shred command in the left pane of the still-open Nautilus Actions window will now no longer be in italics. Click the **Close** button in that window.

To put shred to work in its new graphical manifestation, you must first log out and log back in to your account. After, that just right-click a file you want to shred, and then select **Shred** from the pop-up menu (Figure 19-12). The file will be securely, and permanently, deleted. Decidedly codify.

![](img/f7cef0df22f9dba5a41777808c98eece_390_0.png)

*Figure 19-12: Invoking the shred command via Nautilus*

## 20

## A COLONY OF PENGUINS

*The Ubuntu Community*

![](img/f7cef0df22f9dba5a41777808c98eece_392_0.png)

One thing that really sets open source apart from the commercial software world is the importance placed on the *community*. This can include pretty much anyone who has anything to do with the software: The people who use it, the people who design it, the people who help others with problems . . . every last one of them is a valued community member.

Consider the commercial software world, where things tend to be quite top-down. When you have a problem, you go to some company that provides you with support. This company probably also designed and sold you the software, and you probably played no part in that process—you're the customer; they're the vendor. Open source is different: Rather than one business managing everything, everyone pitches in together and helps each other. People write software and fix faults because it helps other people and because they want to help. Everyone can play their part in offering feedback and suggestions and helping others with problems, and no one is in absolute control of the whole process. All in all, it's much more democratic and, in my opinion, much more fun!
