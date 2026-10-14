
## 9D-5: Cleaning Up and/or Uninstalling Xmahjongg

Once you are done and everything seems to be working as it should, you would normally tidy things up in the Xmahjongg folder by getting rid of any unnecessary files. You can do this via the Terminal by using the cd command to go back into the Xmahjongg folder, typing make clean, and then pressing ENTER.

If you want to uninstall Xmahjongg, open a Terminal window, go back to the Xmahjongg folder by using the cd command, type sudo make uninstall, and finally press ENTER. The routine is essentially the same for any applications installed in this way, though as you might imagine, uninstallation isn’t always as smooth a process as what I’ve just described (and it’s definitely not as easy as it is via the Ubuntu Software Center).

The main reason for the uninstallation process being less than cooperative is that the make uninstall routine requires you to keep the original project folder, which means you have to keep a bit of clutter you normally wouldn’t need to bother with. On top of this, some projects do not provide a make uninstall routine at all. This means that you have to keep track of where everything has been installed in your system and then remove each item using a series of sudo rm commands.

All that negativity aside, go ahead, have some fun, and put your command-line skills to the test. You’ll have something to tell your grandkids about in the future.

## Customizing the Terminal

The Terminal is a very simple application in terms of looks, though you can spice things up a bit if you’re so inclined. Not only can you change the background and text colors in the Terminal, but you can even display one of your favorite photos as a background (as shown in Figure 9-19) or make the background transparent.

To change the Terminal background, go to the Terminal, and select Edit ▸ Profiles. When the Profiles window appears, select the profile you want to edit, which the first time out would be Default, and then click the Edit button. In the Editing Profile window that appears, click the Background tab, select Background image (Figure 9-20), and then navigate to the photo you want to use as your background by clicking the Menu button next to the words Image file and then finding the file in the Select Background Image window. When you’ve found the photo of your choice, click Open. Depending on the image you use for your background, you may find it rather difficult to see the text once your image appears in the Terminal. If so, try moving the slider under the words Shade transparent or image background in the Editing Profile window. If that still doesn’t do the trick, click the Colors tab, deselect Use colors from system theme, and then try some of the preset Foreground and Background combinations from the menu button next to the words Built-in schemes.

![](img/f7cef0df22f9dba5a41777808c98eece_227_0.png)

Figure 9-19: A Terminal window with customized background and font colors

![](img/f7cef0df22f9dba5a41777808c98eece_227_1.png)

Figure 9-20: Customizing the Terminal window

If you just want to make the background transparent, go back to the Background tab, select Transparent background, and drag the slider to the right. You can also use the slider to adjust the shading of your background image if you choose to go that route.

Depending on the colors present in your background image or in your desktop wallpaper (if you’ve gone the transparent route), you may also want to change the font color for your Terminal to make things easier to see. To do this, click the Colors tab, deselect Use colors from system theme, and then make the appropriate font color selection.

## Tabbed Shell Sessions in the Terminal

To wrap things up in this chapter, I thought I might mention one particularly convenient feature of the GNOME Terminal: tabs. Just as you can view multiple web pages in one Firefox web browser window through the use of tabs, tabs in the Terminal application allow you to have more than one shell session running at the same time without having more Terminal windows open (see Figure 9-21). This reduces the amount of desktop clutter and generally makes things easier to deal with. You can open a new tab within the Terminal by going to the Terminal and selecting File ▸ Open Tab.

![](img/f7cef0df22f9dba5a41777808c98eece_228_0.png)

Figure 9-21: Running multiple shell sessions in tabs within the GNOME Terminal
