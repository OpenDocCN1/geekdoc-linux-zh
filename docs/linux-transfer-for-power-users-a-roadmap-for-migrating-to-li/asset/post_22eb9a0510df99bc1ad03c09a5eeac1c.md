
warn you about the one-in-a-thousand situation, rather because you should worry. In practice, I’ve found that Microsoft Office–formatted files are more compatible with OpenOffice.org than they are with other versions of Microsoft Office!

If you are going to be using the revision-tracking feature of OpenOffice.org (found under Edit | Changes), you might want to set some preferences under the OpenOffice.org node, User Data subnode. If you don’t at least enter your name and initials, your changes will appear to other users to have been made by Unknown User, which may or may not be what you intended.

Also under the OpenOffice.org node is the Paths subnode. In this screen you can define where OOO looks for files. You may want to tweak some of these paths depending on your particular needs. I already discussed the default save path—the My Documents type. If you use your own document templates, you may not want to store them in the default location of `/usr/lib/openoffice/share/template/english`. I don’t, because it’s a bad idea to keep your own data buried in the bowels of program directories. I keep all my own templates in a directory on the file server where everyone can access them, and where I can easily back them up.

There are already some templates in the default directory, supplied by the OOO installation. You don’t necessarily want to lose access to those; conveniently, you can add your own template path to the existing path. Select the Templates type from the list, click Edit to display the Select Paths dialog, and then click Add. Use the file drill-down box to select the folder you want to add to the path. See Figure 9.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_216_0.png)

**Figure 9.** You can add your own template directory to the template path.

I tend not to mess with the rest of the options because they’re generally set to the way I work. You should scan through them to see if there are specific settings that you want to change to your preferences.

### Configure

The other mechanism you can use to configure OOO is located under Tools | Configure. Here you can customize the appearance of the OOO screen interface and how the keyboard works. You can determine what toolbars are visible, what buttons they have on them, what keyboard shortcuts do what, and even customize the existing menus and create your own menus.

Again, I try not to spend too much time customizing, because that fine-tuning becomes an impediment if I have to work on someone else’s machine. There are only two changes I make. The first is to modify the Function toolbar (it’s the one with the icons for New, Save, Print, and so on—you know, commonly used functions) at the top of the OpenOffice.org desktop. I add buttons for Document Properties and Insert Graphics because when I’m writing, I use those functions a lot. I also change the mapping of a couple of keyboard shortcuts to represent operations I do a lot.

To add a button to the Function toolbar, select Tools | Configure (or right-click anywhere on a toolbar and select Configure). Select the Toolbars tab of the Configuration dialog, highlight the Function Bar item, and click the Customize button on the right to open the Customize Toolbars dialog. Scroll down through the “Available buttons” list on the left to the Insert node, and then highlight Insert Graphics as shown in **Figure 10**.

Note that you can also remove a button from a toolbar in two ways. The first is to simply uncheck the check box. The button will stay in the list but won’t appear under the toolbar. This technique is handy for temporarily hiding a button. If you’re darn sure you don’t want the button again, you can highlight the button label in the “Buttons in use” list and then click the Remove button. (You can get it back by adding it from scratch, as I described earlier when discussing the Insert Graphics button.)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_217_0.png)

**Figure 10.** Adding a button to a toolbar.

I use the Edit | Repeat command a lot, but I don’t like using the keyboard or mouse to do it. I’d rather just hit a function key. So I reassigned F12 to execute the Edit | Repeat command. The interface for reassigning keys is a little awkward. In order to modify a keyboard shortcut like this, open the Configuration dialog via the Tools | Configure menu option, and then select the Keyboard tab.

Next, in the “Shortcut keys” list, highlight the key you want to assign to a command. On the right side of the list, you may see a command already assigned to the key. Use the Functions area in the bottom half of the Keyboard tab to select the command you want to assign. First, select a category from the Category list (in this example, that would be Edit). The choices that appear in the Function list change according to which category you select. Then select a function (in this example, that would be Repeat). The Configuration dialog looks like Figure 11 at this point.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_218_0.png)

**Figure 11.** Assigning the Edit | Repeat command to the F12 key.

Finally, click the Modify button, and you’ll see two things. First, the key you selected (in this example, F12) will appear in the Keys list. Second, the F12 key will have a command associated with it in the “Shortcut keys” list in the top half of the Keyboard tab. See Figure 12.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_219_0.png)

*Figure 12.* The newly assigned F12 key now will execute the Edit | Repeat command.

You can perform similar modifications to the menu and to the status bar by using other tabs in the Configuration dialog.

### The OpenOffice.org interface

The OpenOffice.org interface looks pretty much like any other graphical office suite, with a menu and one or more toolbars above the work area, whether that space is a writing area, a grid of spreadsheet cells, or a presentation or drawing canvas.

OpenOffice.org features an additional toolbar, called Main, which resides to the left of the work area. Its specific functions vary according to which kind of application you’re working in. In Calc, the icons in the Main toolbar provide one-click access to functions such as Insert, Insert Cells, Insert Object, Spell Check, Find, Filter, and Sort. In Writer, however, the icons represent different functions, such as Insert Table, Insert Auto Text, Spell Check, Find, Show Nonprinting Characters, Show Graphics, and Show Online Layout.

Some menu items are disabled depending on which functions are selected in the various toolbars. For example, if you have selected Show Online Layout, your document will appear as one long document without page breaks—as if you were typing on a roll of towels. In this mode, you can’t do a print preview.

While there seems to be a zillion (plus or minus a couple) icons, menu options, functions, and other goodies in the OpenOffice.org suite, implementations of two specific functions bear special mention.

The last two icons in the standard Function bar are the Navigator (a spiral-shaped star) and the Stylist (a finger pushing up one of two buttons). I’ll cover the Stylist first because one of its features is used with the Navigator.

### The Stylist

If you're not familiar with styles and templates, a brief sojourn is in order, and will be well worth your while. A paragraph style is a collection of formatting attributes that are given a single, specific name. For example, you could create a custom look for a paragraph that specified a 28-point font, bold, and left-aligned. Instead of manually applying those attributes to each paragraph that you wanted to look like that, you just apply the style to a paragraph, and voilà! The paragraph now has all those attributes. Even better, should you decide that all of those paragraphs should really be 30 points instead of 28, you only have to change the style, and the paragraphs themselves will automatically inherit the new attributes. The name of each chapter in this book has a style called "chaptitle" that has those attributes.

You can create a special type of document called a template that contains a group of styles—for example, the template used for this book has styles for various levels of headings, paragraphs that directly follow a heading, body paragraphs, figure captions, and so on. Using a template makes it a lot easier to create a long document (or multiple documents) because you can simply apply a style to a paragraph and you know it will be consistent with all of the other paragraphs formatted with the same style.

The Stylist is a tool that helps you use styles (either native OpenOffice.org styles or your own) in your documents. Clicking the Stylist button (or selecting Format | Stylist, or pressing F11) displays a list, as shown in **Figure 13**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_220_0.png)

**Figure 13.** The OpenOffice.org Stylist displays a list of available styles.
