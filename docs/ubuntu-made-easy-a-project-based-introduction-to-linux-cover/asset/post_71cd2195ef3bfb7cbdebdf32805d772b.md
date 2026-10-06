
escputil This works for some Epson printers and is worth a try if Mtik doesn't support your model. Open the Ubuntu Software Center and install escputil. Then open a Terminal by searching for Terminal in the Dash. Type escputil -i (don't forget the space) and hit ENTER to display the ink levels. To clean the print head, use escputil -c.

If you have no luck with these utilities or if your printer's make isn't listed, you might still be able to access ink levels and maintenance functions using the manufacturer's own Linux driver, if one exists. Also, some newer printers allow you to check ink levels and align clean cartridges controls on the printer. In doubt, check your printer's manual.

## Project 10: Installing TrueType Fonts

On some level, printing is all about presentation. If you're going to all the trouble of printing something out, it's more likely that you want it to look good. Few things affect presentation more than your choice of font: Unless you're a children's entertainer, you probably won't get far with a wacky font Comic Sans on your résumé., a medieval-looking gothic font would probably be wasted on that letter to your bank manager. Fortunately, your Ubuntu system comes with a wide variety of usable and, at my eyes, handsome TrueType fonts. However, these need to be on the conservative side of the aesthetic spectrum, and many users will want to add a few more distinctive fonts to the system repertoire.

Your bank manager may not appreciate that Gothic font, but you may want to print an award for an event you are hosting. Or you might be preparing a newsletter for the local chapter of your snail-breeders and want to use a font that is round, bubbly, and slimy. Whatever your penchant, purpose, or desire, you will probably reach a point when you want to install some other TrueType fonts on your system, in this project I'll tell you how to do it.

How you install fonts depends on who is going to use them. If you have only one user account on your machine, the easiest is to install the fonts locally, as described in "10-2: Installing Fonts" on page 191. Locally installed fonts are ones that only you or someone logged in to your user account will be able to use. On the other hand, if you have more than one user account and want the fonts to be available to all the users on your machine, you'll need to install them globally—in this case, see "10-3: Installing TrueType Fonts Globally"

## 10-1: Getting the Font Files

The Internet is awash in free fonts. For this project, I will point you to the http://www.fontfreak.com/site, which has a very nice collection of fonts. Once you get to the Font Freak home page, click the Fonts link under the "FREE FONTS" heading on the left side of the page. The next page will ask you whether you want to download all the free fonts on the site in one single file; click No thanks, I will download them one by one. This will lead you to the main list of free fonts; browse through the various pages until you find that is to your liking and click it. Which font you download is completely up to you, but be sure to choose the PC version, not the Mac version. You can do this by clicking the small Windows icon immediately to the right of the font's name. When the download window pops up, choose Save File and click OK to save the font as a Zip file. To follow along with this project, download a couple of fonts—I chose Aajax Surreal Freak and Accidental.

When you're finished downloading, drag the font folder (or wherever you saved them) to your Home folder so it's easy to copy along my instructions. Also, be sure to unzip font files before going on the installation steps. (Right-click each Zip file and choose Extract Here.)

## 10-2: Installing Fonts Locally

If you're the sole user of your computer, installing fonts locally will just do fine. To get started, you need to set up your system by providing it with a location for your fonts. You will need to do this the very first time.
Here's what you do:

- 1. Open your Home folder and, in that, create an invisible folder by selecting File ▸ Create Folder.
2. When the folder appears, name it .fonts (the period before the name means it will be hidden).
3. Hide the new folder by selecting Edit ▸ Reload. Your .fonts folder should no longer be visible. If this is the case, you can close the window—your setup was successful.

Now that everything is set up, let's continue with this project using one of the fonts you downloaded. After you've decided which font to use, follow these steps:

- 1. Choose the unzipped font file (its name probably ends in .ttf), and copy it by right-clicking and selecting Copy.
2. Press CTRL-L or select Go ▸ Location. This will display the location bar in Nautilus.
3. In the location bar, type "~/fonts and press ENTER. The ~ sign is a short-cut that means "My Home folder".
4. You should be taken to the empty .fonts folder you just created, like the one in Figure 10-9. Right-click anywhere in the folder and select Paste to copy the font into the folder.

Now that you have installed your font, you can give it a try in one of your applications, such as LibreOffice Writer. (Any running applications needs to be restarted before the new font will appear in that application's font menu.)

![](img/d35fa962e6f9664d66dc83916f426418_229_0.png)

## 10-3: Installing True Fonts Globally

As I mentioned earlier, the font you just installed locally can be used when you log in under your usual username. If, however, you want to install fonts that can be used by you and anyone else who has an account on your computer, the process is slightly different and will require a little “superuser” action. You can use the other font you downloaded for this part of the project.

The folder for globally installed fonts is in root territory, you will need to open the file browser as superuser in order to install the fonts. Superuser is another name for the root (administrative) user. It's possible to run a program without switching to a different user account by using a system called sudo (discussed in Chapter 8), but since root can modify system files, you shouldn't run a program in sudo mode unless you absolutely must.

Here are the steps for getting your font file into the global directory:

- 1. Press ALT-F2 and then type `ksudo nautilus /usr/share/fonts/truetype` into the box that appears. Press ENTER and type your password when prompted.
2. A file browser will open. Select **File ▶ Create Folder** to create a new folder; call it *MyFonts*.
3. Open a normal file browser (Nautilus) by right-clicking the **Nautilus** icon on the Launcher and selecting **Open a New Window**. The `.ttf` font file you want to install, and copy it (for example, by right-clicking it and selecting **Copy**).
4. Switch back to the Truefile browser window, open your newly created *MyFonts* folder, and paste the font into it.
5. Be sure to close the superuser file browser window—leaving it open is a recipe for disaster!

NOTE The gksudo command in Step 1 is the graphical environment version of the nongraphical sudo command that you saw how to use via the command Terminal in Chapter 8.

Now you can test things by opening LibreOffice and looking for the font in the menu. Remember that you will need to restart LibreOffice if it was already open when you installed the font.

## Scanners

Scanners are extremely useful and about cheap a peripheral device you can get. They allow you to put images or pages into digital text into your computer—much the same way you would duplicate a document on a copy machine.

Even though scanners have been around for a relatively long time, support for them in Linux is still a bit spotty. Frankly, this is for the better with every new Linux release. The backend—the hidden part of your system that handles scanner recognition and support—is called Sane. If you are wondering whether Linux will be able to recognize your scanner or if you are trying to figure out what scanner to buy, you can visit the Sane website at http://www.sane-project.org/sanemfgs.html. The page is pretty long, so you might want to find the function in your web browser to search for your scanner model. As I have mentioned, you can also try the Ubuntu forums (http://www.ubuntuforums.org/) for Ubuntu-specific recommendations there.

## Scanning, No Questions Asked, with Simple Scan

Simple Scan is a relatively new addition to Ubuntu's default applications, and it lives up to its name—it doesn't take many clicks to get a document from scanner bed to computer screen. To run Simple Scan, make sure your scanner is connected and switched on then open Simple Scan from the Dash. If you get a warning saying that no scanners were detected, skip to "Unrecognized Scanners" on page 196.

Assuming that your scanner has been recognized, you will be presented with the screen in Figure 10-1.

It's pretty easy from here—select the type of document you're scanning (Text or Photo) from the drop-down menu next to the Scan button (menu icon is a small arrow) and then click Scan. Your scanner will roar into action, and after a short wait, you will be presented with a preview of the picture or document you placed on the scanner. You can crop and rotate the image by using the Pages menu or by right-clicking the picture. When you're happy with your scan, select Document > Save to finish it.

One little tip: To change the resolution of your scan, select Document > Preferences and tweak the settings in the window that appears. Higher resolutions can take longer to scan and take more disk space, but choose wisely!
