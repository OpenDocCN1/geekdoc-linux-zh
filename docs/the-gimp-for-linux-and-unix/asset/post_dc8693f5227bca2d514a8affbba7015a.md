
# Table of Contents

- Give an image the appearance of motion ........................................................ 238
- GIMP filter guide ..................................................................................... 239
- Artistic filters ................................................................................ 239
- Blur filters ....................................................................................... 239
- Colors filters ................................................................................. 240
- Combine filters ............................................................... 240
- Distorts filters ............................................................................... 241
- Edge-detect filters ................................................................ 242
- Enhance filters ................................................................ 242
- Glass effects filters ............................................................ 243
- Light effects filters ............................................................. 243
- Misc filter ....................................................................... 243
- Map filters ...................................................................... 244
- Noise filters ................................................................... 244
- Render filters ................................................................... 245
- Some filter combinations ................................................... 246

# Chapter 16 Plug-ins and Script-fu 247

- View installed plug-ins and script-fu ................................... 248
- Create a geometric shape with Gfig ............................................ 249
- Create a geometric pattern with IfsCompose ................................... 252
- Find and Install more plug-ins ................................................ 253
- Incredible script-fu ............................................................ 254
- I want to write my own script-fu! ........................................ 254
- Add coffee stains to an image .................................................. 255
- Make an image look like an old photo ........................................ 256
- Quickly add a border around an image ................................ 257
- GIMP script-fu guide ............................................................ 258
- Decor script-fu ................................................................. 259
- Alchemy script-fu ............................................................. 259
- Animator script-fu ............................................................. 259
- Modify script-fu ............................................................... 260
- Render script-fu ................................................................ 260
- Shadow script-fu ............................................................... 260

# Chapter 17 Creating Images for the Web 261

- Ruler units and image resolution ................................... 261
- Convert an image to indexed color .......................................... 262
- To dither or not to dither? ................................................... 263
- View and edit the color palette created from an indexed image ................................................................ 264

![](img/5164bc49fb24f10213e18cc994b7b40c_14_0.png)

# Table of Contents

- View the Web color palette ................................................... 265
- Create a background .............................................................. 266
- Web graphics and file size ................................................. 266
- Help with Web design ........................................................ 267
- Use a script-fu to create Web page elements ................................................................ 268
- Create graphics quickly using the Web ........ 269
- Save a graphic as a .gif file ................................................ 270
- Save a graphic as a .png file ................................................ 272
- Save a graphic as a .jpg file ................................................ 273
- More information on creating ............................................ 274
- Web pages ................................................... 275
- Good Web site and page design ................................... 275
- Create a simple animation ........................................ 276

# Chapter 18 Printing and Output 281

- Create images that print well ................................... 282
- Scale an image using cubic interpolation ........................................................ 284
- Print an image ....................................................... 285
- Select a different printer ......................................... 286
- Set a different page size, paper, or orientation ........................................................ 287
- Select a different printer tray ................................... 287
- Set a printer resolution ....................................... 288
- Scale down an image to a specific percentage or resolution ................................... 288
- The colors on the printed page don't match the colors on my monitor ............... 289
- Adjust the brightness of a printed image ................................................... 289
- How does offset printing work? ............................ 290
- Preparing an image for a service bureau ................................................ 291
- Generate a .ps or .eps file ................................... 291

# Appendix A Glossary 293

# Index 297

# THE BASICS

Welcome to the amazing world of the GIMP! The GNU Image Manipulation Program (fondly called the GIMP) offers a professional set of tools for creating and manipulating images. This program has incredible power and loads of features, all incorporated in an interface that is way cool. You can run with the GIMP as far as you please. With the GIMP and your imagination, the sky's the limit!

So, just what is the GIMP? The GIMP is a pixel-based image manipulation program (also called a bitmap or raster program). In the GIMP (and other pixel-based programs such as Adobe Photoshop and Corel Photo-Paint), images are made up of tiny dots pixels. These pixels are arranged in horizontal and vertical rows, and are colored to create a pattern. The shape and color of a pixel-based image appear smooth from a distance, but if you were to view a pixel-based image close up, you would see tiny individual squares. Pixel-based images depend on the resolution at which they are saved for printout quality.

My purpose in writing this book is to show you how easy it is to create amazing imagery with the GIMP. In keeping with the Visual QuickStart Guide format, my aim is to present easy, step-by-step directions with illustrations to take the mystery out of the most complicated feature.

If you are new to the GIMP, the program may seem a bit dense at first because it is so rich in features. But, if you take it one step at a time, you'll be creating beautiful images in no time. For those of you who are already acquainted with the GIMP, use this book as a guide to discover new features and techniques, and as a handy reference.

Have fun!

![](img/5164bc49fb24f10213e18cc994b7b40c_16_0.png)

# Is the GIMP Installed?
(And What to Do)

## Working with Scanners, Digital and Video Cameras, and Drawing Tablets

Whether the GIMP was installed or not depends on the selections you made during installation. A missing menu item does not necessarily indicate the absence of GIMP; it may not have been added to the menu.

Scanners, cameras, pens, and other pointing devices are great for creating digital images that you can use in the GIMP. Unfortunately, you can't just plug a peripheral and have it automatically work; compilation is different for each platform and is beyond the scope of this book, but I will give a brief description of what's needed for each.

- Look on the menus on your desktop. If you find a GIMP item, select it to launch the GIMP.
- If a menu item isn't present, use File Manager to find gimp is present in /usr/bin/. If the gimp file is there, double-click to start the GIMP.
- If a menu item is not present and you can't find the GIMP file in /usr/bin, then the GIMP probably has not been installed. You can check this by running GIMP and seeing whether the GIMP package is installed. It should be listed with the Multimedia packages in the Applications hierarchy.
- If the GIMP is not installed, then you will have to install it from the RedHat Linux 6-ROM.
- If all else fails, you can download the recent stable version of the GIMP from http://www.gimp.org/download.html. Instructions for installing the GIMP can be found at http://www.gimp.org/install_help.html

Digital scanners as either parallel or SCSI interfaces, though a scanner with a SCSI interface is the easiest to configure and use with the GIMP. SANE (Scanner Access Easy) is the universal scanner interface that is most frequently used with the GIMP. To find out which scanners are supported by SANE, and how to compile, install SANE, go to http://www.mostang.com.

Digital and video cameras with a camera hooked up to a parallel port and the appropriate driver installed, the GIMP can be used to capture digital and video snapshots. To find out what's supported, go to http://metalab.unc.edu/pub/Linux/video/!index.html.

Wacom pen and other drawing tablets needs to be recognized by X Windows before the GIMP can use this device. In addition, you'll need to have a recent version of the GIMP Toolkit (GTK) installed on your computer so the GIMP supports Input. For Wacom driver, go to http://www.lepied.com/xfree86/. Check out http://www.gtk.org/ for the latest version of the GTK.
