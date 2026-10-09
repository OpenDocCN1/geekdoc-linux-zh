
# COLUMNS
## COOKING WITH LINUX

Tools like KCharSelect and Gucharmap are wonderful to have at your disposal, but for some people, there is only an occasional need for entering special characters.

![](img/526fd434dcfcf1b461b94c24ea170f36_27_0.png)

Modify the character list to suit your taste or need, then click OK. You may want to use KCharSelect, just this once, to paste in your list of characters.

Those of you who are running GNOME as your default desktop environment have a similar tool at your disposal, and it also is an applet. Right-click on the bottom (or top) panel and select Add to Panel. A window of the same name appears with a list of available applets (Figure 7). Scroll down until you see the Utilities section. There you will find an applet named Character Palette. Select it, then click Add or simply drag the applet to the panel in the location of your choice.

![](img/526fd434dcfcf1b461b94c24ea170f36_27_1.png)

You will see a row of characters appear on your panel with a drop-down arrow to the left of those characters. To use any of these characters in a document (or e-mail message or chat session or other application) click the character of your choice, then paste it into your application. If you don't see the character you need, there's a good chance it already has been defined for you. All you need to do is switch palettes. Click the down arrow, and a selection of more than 20 predefined palettes appear; simply click to switch. As rich as this selection is, it still is possible that the characters you need on a day-to-day basis are not there. To edit the palette or add to it, right-click on the down arrow and select Preferences from the submenu. The Character Palette Preferences dialog appears (Figure 8).

![](img/526fd434dcfcf1b461b94c24ea170f36_27_2.png)

From this dialog, you can choose to edit a current palette, delete a palette or create something entirely new. To create a new palette, click the Add button and enter the characters into the dialog window that appears—of course, you may need to paste them from another character application, such as Gucharmap or OpenOffice.org.

Now, when François becomes a master of Spanish, he will be able to enter all the Spanish characters he wants. In the meantime, mes amis, it appears that it is nearly time to bid you all Adieu. Nearly, being the key word, or as François might now say it, casi. Quoi? You plan on learning Japanese next week? Why not. Until next time, please raise your glasses, mes amis, and let us all drink to one another's health. A votre santé! Bon appétit!...

Marcel Gagné is an award-winning writer living in Waterloo, Ontario. He is the author of the all-new Moving to Free Software, his sixth book from Addison-Wesley. He also makes regular television appearances as Call for Help's Linux guy. Marcel is also a pilot, a past Top 40-disk jockey, writes science fiction and fantasy, and holds a mean O'Grand 1-Rex. He can be reached via e-mail at mgagne@salmar.com. You can discover lots of other things (including great Wine links) from his Web site at www.marcelgagne.com.

### Resources

- GNOME Web Site: www.gnome.org
- Gucharmap: live.gnome.org/Gucharmap
- KDE Web Site: www.kde.org
- OpenOffice.org: www.openoffice.org
- Marcel's Web Site: www.marcelgagne.com
- The WFTL-LUG, Marcel's On-Line Linux User Group: www.marcelgagne.com/wftlugform.html

# SUPERMICRO®

## UIO

### Universal I/O

*Maximized I/O Expandability & Flexibility*

# The Freedom to Build Exactly What You Need.

- 3/7" Add-on Cards for 1U/2U
- Highly Upgradeable
- High Efficiency Power (up to 90%+)
- Multiple Expansion Card Options (SAS RAID 5, 10-G, IB...up to 20 choices)
- Simplify Your Inventory Management

![](img/526fd434dcfcf1b461b94c24ea170f36_28_0.png)

Supermicro SAS RAID 5 card.

# Available Motherboard Options

![](img/526fd434dcfcf1b461b94c24ea170f36_28_1.png)

# Optimized Chassis Solutions

![](img/526fd434dcfcf1b461b94c24ea170f36_28_2.png)

Supermicro UIO servers allow users to select from a wide range of I/O options to provide the ultimate in storage and networking flexibility. The UIO card becomes a part of the serverboard, allowing the system to retain all of its PCI Express and PCI X slots for expansion cards. As a result, future upgrades can be achieved by replacing the UIO card and/or expansion cards instead of replacing the entire system. This versatility helps to minimize the amount of different servers that customers need to operate their business.

![](img/526fd434dcfcf1b461b94c24ea170f36_28_3.png)

For more information visit us at www.supermicro.com

* Our new generation power supply efficiency measures 90%+ or more under a typical loading operation.

# WORK THE SHELL

![](img/526fd434dcfcf1b461b94c24ea170f36_29_0.png)

## Dave Taylor

### Displaying Image Directories in Apache, Part III

The incredible shrinking script knows a better way to resize your thumbnails.

In last month's column, we built our directory display script to the point where you could get a smart listing that showed your image files (offering links to any other file type), and we allowed thumbnails to be displayed too.

The latter trick is done by letting the Web browser do the work. If you specify a height or width that's different from the actual image size, Web browsers automatically scale the image to fit the specified dimensions. Even better, if you specify only one dimension, it scales proportionally to fit.

Let me explain that just a wee bit more, because it's critical to this particular scripting project. If you have an image that's 250x250 pixels and you'd like to display a 75x75 thumbnail, the best practice is to specify both height="75" and width="75", of course. The problem is, what if the image is actually 250x317 and you want to reduce it to exactly 75 pixels wide. How tall should it be?

You could do the math, of course, but it's much nicer to let the browser do the work for you automatically, which happens if you specify only width="75" or use a full HTML statement:

```html
<img src="my250x317.png" width="75" />
```

Doing that scales it, and you end up with an image that's exactly 75x95 pixels in size. However, if you always constrain one dimension, things can break. What if the image is actually 250x1100, because it's a very tall graphic? Now the thumbnail is going to break the entire layout, because the scaled version of it is 330 pixels wide, quite a bit more than the 75x75 target box for the image!

That's why an ideal script would figure out which of the dimensions is larger, and then constrain that one to the size of the box we seek, letting the other scale proportionally automatically, thanks to the Web browser. And, that's exactly what we'll do!

**Big Important Caveat:** I realize there's a significant performance penalty for letting the browser scale images—the entire full-size image has to be downloaded, even though you're seeking a smaller version. If it was a problem, you could use a tool such as ImageMagick to scale the images and create thumbnail graphics that were displayed instead, probably dropping them into a cache and creating new ones on the fly as needed. But honestly, don't you have a high-bandwidth Internet connection, and does an additional second or two of load time really matter?

## On to the Script!

Last month, we created the darn useful function figurerize, which, when given a graphic image, returned height and width parameters than those could be calculated. The resultant main loop in the script ended up looking like this:

```bash
for name in *
do
    if [ ! -z "$(file -b $name|grep 'image data')" ]
    then
        figurerize $name
        if [ ! -z "$height" ] ; then
            echo "<img src=$name alt=$name height=50 />"
            echo "<br />$name ($height x $width)<br />"
        else
            echo "<img src=$name alt=$name height=50 />"
            echo "<br />$name<br />"
        fi
    else
        echo "<a href=$name>$name</a><br />"
    fi
done
```

If you read the code closely, it's really not doing anything smart with the height and width parameters, just displaying them in the output. Instead, let's turn that into a test to figure out which is larger. Before I do that though, we need to make some rudimentary improvements to the loop so the output is more attractive:

```bash
for name in *
do
```
