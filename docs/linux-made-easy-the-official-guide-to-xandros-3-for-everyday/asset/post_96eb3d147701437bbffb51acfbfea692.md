
If the title of an email contains the word “virus,” even if it is from someone you know, then it is probably best to be suspicious of it also. After all, even if a message titled “Help, I think I’ve got a virus!” is legit, it would indicate that the sender’s system is infected, right?

Okay, so now that I’ve hopefully instilled a useful level of paranoia in you, let’s get on to dealing with legitimate, nonviral attachments, starting with opening and saving those that you receive.

## Opening and Saving Received Attachments

When you receive an attachment, you’ll know because the title of the mail will have a small paper-clip icon next to it (Figure 13-20).

![](img/3badae5570de77b990135448f8a8a1cc_255_0.png)

Figure 13-20: Thunderbird lets you know when you have received an attachment

In addition, a small box will appear at the bottom of the email message in an Attachments box, displaying the name of that attachment, as you can also see in Figure 13-21. If the attachment is a graphics file, such as a digital photo, the image will also appear within the email message area.

You have two ways to deal with the attachment, both of which involve right-clicking the filename in the Attachments box at the bottom of the window. When you do this, a pop-up menu will appear, and from that menu you can select either Open, after which a window will appear asking you which application to use in order to open the attachment, or Save As, which is the preferred method. When you select Save As in the pop-up menu, the attachment will be saved to your hard disk, from which you can do with it as you see fit. Of course, if the attachment is just a picture, you can just view it in the message area and leave it at that if you have no interest in saving it for future viewing or use.

## Sending Attachments

If you want to send your own attachment, simply click the **Attach** button in the Compose window for the email message you are writing, and then navigate to and select the file you want to attach in the Attach File window that appears. If you would like to attach more than one file, you can do so by holding down the CTRL key and then selecting each of the files you want to attach (Figure 13-21).

![](img/3badae5570de77b990135448f8a8a1cc_256_0.png)

*Figure 13-21: Sending email attachments in Thunderbird*

When you have finished making your selections, release the CTRL key (if you were selecting more than one file), click the **Open** button, and the files will then be attached to your email message. Once you send that mail, the job will be done.

## 13A-3: Dealing with Spam in Thunderbird

Well, if you are anything like the millions of other email users in the world today, you are probably deluged every week with hundreds of unwanted and uninvited email messages announcing that you qualify for a mortgage, offering you low-cost prescription drugs, telling you how you can get an online degree, or advising you where you can meet singles in your area. Yes, such are the wonders of the greatest nuisance foisted upon society since the heyday of telemarketers: *spam*.

Fortunately, Thunderbird helps reduce the annoying effects of spam by means of its *Junk Mail Controls* feature. Thunderbird’s Junk Mail Controls feature is essentially an adaptive filter that tries to determine which of your email messages are spam. At first, it is none too clever and marks many a good message as junk, while leaving some junk messages as is. You will know when Thunderbird has marked a message as junk by the trash can icon in place next to the sender’s name in the list of email messages in the main window (Figure 13-22).

![](img/3badae5570de77b990135448f8a8a1cc_257_0.png)

Figure 13-22: Marking or unmarking messages as junk

If Thunderbird has made a mistake, you can correct it by clicking the icon when a message is not junk or by clicking the small dot icon if the message should be marked as junk (also seen in Figure 13-23). Through time, Thunderbird learns what is junk and what isn’t (hence the *adaptive* bit I mentioned), eventually getting it right most of the time. When you are satisfied that Thunderbird is getting things right most of the time, you can set up the Junk Mail Controls to automatically load any incoming email deemed to be junk in a special junk folder.

You can set it up to automatically reroute such mail to the Junk folder by going to the **Tools** menu and selecting **Junk Mail Controls**. When the Junk Mail Controls window appears (Figure 13-24), click the box next to *Move incoming messages determined to be junk mail to*:

![](img/3badae5570de77b990135448f8a8a1cc_257_1.png)

Figure 13-23: Setting up Thunderbird to automate the junk-mail-handling process

The other settings should already be correct, so just click the **OK** button, and your world, at least the world of your inbox, will become a much happier and less-cluttered place.

Of course, spam from new sources will arrive from time to time, so you might still have to mark certain items manually as junk. When you do that, on this point however, those messages will be automatically moved to the junk folder. It is also a good idea to check through the junk folder before trashing its contents—just to make sure that no good messages are inadvertently being placed there.

## 13A-4: Using Folders in Thunderbird

When you receive a lot of mail from a particular sender, it can be useful for you to set up a folder for that sender. This is especially handy if you happen to subscribe to one or more mailing lists, whose string of messages can quickly fill up your inbox. Just go to the **File** menu and select **New ➤ New Folder**. After that, a small window will appear in which you type in a name for the folder and then click **OK**. The folder will then appear in the left pane of the Thunderbird window. Once the folder is in place, you can simply drag all the email that falls under the category you’ve just created into the folder.

A still easier way to do this is by typing the name of the sender or group in question in the search box near the top-right corner of the window. Once you do that, only the messages matching that entry will appear in the list of email messages below (Figure 13-24).

![](img/3badae5570de77b990135448f8a8a1cc_258_0.png)

If you then click one of the messages in the list, and choose **Select ➤ All** in the **Edit** menu, you can easily select all of these messages in one go. Dragging them to the new folder thus becomes a much easier chore, so all you have to do is click any one of the now-highlighted messages and drag the whole lot into your new folder.

## 13A-5: Creating a Message Filter in Thunderbird

If you would like to automate things a tad so that certain messages are automatically loaded to your new, or some another, folder in the future, you can create a message filter. To do this, start out by going to the **Tools** menu and selecting **Message Filters**. Once the Message Filters window appears, click the **New** button, which will bring up the Filter Rules window, shown in Figure 13-25.

In that window, here’s what you have to do:

1. In the uppermost text box, give your new filter a name.
2. In the same window, choose a surefire way to distinguish the messages that you would like to be automatically loaded into the folder upon arrival. For example, let’s say that you created a folder for one of the mailing lists to which you belong. The subject lines of most mailing-list messages are preceded by the name of the list in brackets, such as [Music Lovers] or [Faye Wong List]. Since this is consistent at all mail from the list and is not likely to appear in any of your other e-mail messages, it would be a good candidate for this purpose. That being the case, in the top pane of the Filter Rules window you would select **Subject** in the first drop-down menu, select **contains** in the second, and then in the adjacent box type the bracketed name of the list.
3. In the bottom pane of the window, select **Move to folder**, and then, via the drop-down menu in the middle of the pane, select the folder to which you want the mail moved. In the case of this example, you would be selecting the folder you just created in Project 13A-4.
4. Your Filter Rules window would then look something like that in Figure 13-25. If so, click **OK**. The Filter Rules window will then close, and your new filter will appear in the list of filters within the Message Filters window, which you can then close. Now all of the mail you receive in the future from the person or group specified in your new message filter rule will be automatically rerouted to that folder.

![](img/3badae5570de77b990135448f8a8a1cc_259_0.png)
