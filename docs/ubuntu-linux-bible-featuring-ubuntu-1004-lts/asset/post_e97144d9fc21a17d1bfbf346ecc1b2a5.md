
## Chapter 15: Working with Graphics

### Starting Inkscape

After installing Inkscape, you can start the program in a variety of different ways, the most basic of which are:

- On Ubuntu systems, by selecting Inkscape Vector Illustrator from the Applications Graphics menu
- By typing the inkscape command in a GNOME Terminal or xterm window and pressing Return

The application starts, displaying an empty document, as shown in Figure 15-13.

### FIGURE 15-13

Starting Inkscape

![](img/1a233c34336fbf5a85d6eb785e401709_594_0.png)

### A Quick Tour of Inkscape

Inkscape provides great online help and even includes some tutorials that are available from its Help menu. The callouts in Figure 15-13 highlight the basic components of the Inkscape interface, which are as follows:

- **Menus**: The dropdown menus in Inkscape are organized to provide easy access to commands related to the basic elements of SVG drawings, such as Layer, Object, Path, and Text. The Inkscape designers have done a great job at minimizing the number of submenus used in the program—almost every command is directly available from a top-level menu.

- **Toolbars**: Inkscape provides two horizontal standard file and clipboard manipulation bar, provides access to a variety of commands for zooming, copying, and grouping selected objects. The bottom toolbar, the Tool Controls, provides easy access to rotation, layer manipulation, and scaling commands. Clicking on the arrow down at the right of each of these displays additional, related commands for these toolbars.

- **Toolbox**: A vertical toolbar along the left side of the edit window. The toolbox contains icons for common creation and editing commands, as those for selecting objects; zooming in and out; and creating squares, circles, 3D boxes, various sorts of lines, and so on.

- **Rulers**: These rulers display the horizontal and vertical location of the cursor in the current document.

- **Scrollbars**: Horizontal and vertical scrollbars at the bottom and right of an Inkscape window make it easy to move around zoomed or otherwise large images. If the entire image can be viewed at once, the scrollbars do not appear.

- **Palette**: a palette at the bottom of an Inkscape window makes it easy to select new drawing and fill colors.

- **Status bar**: the status bar at the very bottom of an Inkscape window provides information about the current layer, selected fill color and stroke type, the current X Y cursor position, the current zoom, and so on.

- **Context-sensitive menu**: Right-clicking on any component of a drawing that you are working on Inkscape displays the context-sensitive menu that is also shown in Figure 15-13. This menu provides quick access to several commonly used commands and submenus, including those for duplicating a selected object, grouping and ungrouping, and undo operations, and a general properties panel for the selected object.

You can hide (or subsequently reveal) all of these (except for menus) by selecting the associated items from Inkscape's View Show/Hide Menu. You can also configure Inkscape preferences by selecting the File Ink Preferences menu command. These preferences can be very handy for controlling cursor, scrolling, and selection granularity, which can be critical when dealing drawings in Inkscape.

### More Information about Inkscape

I am not the best graphics artist, I'll leave the evangelizing to those who are. The following are some of my favorite Inkscape-related sites on the Web:

- www.inkscape.org: The home page of the Inkscape project, this page provides access to many Inkscape resources, such as mailing lists, articles, collections of images, and so on.

- www.inkscape.org/mailing_lists.php: Inkscape-mailing lists. The Inkscape-user list is a great place for asking questions and searching for solutions to whatever problem you're experiencing (with Inkscape, that is). The Inkscape-announce list is a low-traffic list, but is worth subscribing to so that you are notified of new major and patch releases of Inkscape.

- http://tvmjong.free.fr/INKSCAPE/MANUAL/html/index.php: Tavmjong Bah is writing a book about Inkscape that is freely available on the Web. This is a great book with a fantastic selection of information.
- www.angelfire.com/mi/kevincharles/inkscape/index.html: An unofficial (but extremely useful!) user manual for Inkscape written by Kevin Wixson.

As with every popular source package, more resources and sources of related information for Inkscape are probably appearing on the Web as I type. If you find a great Inkscape resource that I've missed in this quick summary, please let me know. Inkscape is a great program!

### Other Graphics Applications

Graphics programs seem to rank second to text editors and word processors in terms of the sheer number of available choices. Each has its own niche, fans, and detractors. Since I've already acknowledged that I am not particularly good at graphics, I've covered only the graphics programs that I have actually used at one time or another and I feel that are the best applications for creating and editing various types of graphics on Linux systems. Some other good graphics applications are as follows (all of which are available in the Ubuntu repositories unless noted):

- Blender (www.blender.org): An impressive 3D modeling graphics, rendering, and animation package that has been used to make various animated films, video and desktop computer games, and so on. Blender is also a great tool for architectural or simple wire-frame drawings.
- CinePaint (cinepaint.org): an image-editing application that began life as an earlier version of GIMP, but has since seen a significant amount of development since then, including adding support for 8-bit, 16-bit, and 32-bit color channels and high-quality image formats such as DPX, 16-bit TIFF, and OpenXR. CinePaint has been used in many feature films (the "Harry Potter" films, The Last Samurai, The Lord of the Rings" films), so it's impossible to dispute its quality or its business value.

### Note

CinePaint is not available in the standard Ubuntu repositories but is included in the media-oriented Ubuntu Linux distribution (http://ubuntustudio.org). ■

- Dia (http://1.gnome.org/dia/): A GNOME-based application for creating editing diagrams and flowcharts on Linux systems, similar to and evocative of Microsoft's Visio application. Dia is not installed by default on Ubuntu systems.
- GNU Paint (www.gnu.org/software/gpaint): a simple, GNOME-based application for creating and editing graphics, GNU Paint has all of the attributes of XPaint ancestor, Microsoft Windows Paint, or MacPaint. GNU Paint is easy to use, but primarily because it doesn't do much when compared with the other graphics applications discussed in this chapter. GNU Paint is not available in the standard Ubuntu repositories. I am primarily mentioning here because you might have heard of it, not as a suggestion.

- Xara Xtreme (www.xaraxtreme.org/about/): a vector graphics application that was primarily developed for Microsoft Windows systems (and is still actively supported under development there), Xara Xtreme was released as open source in 2006 and ported to Linux. It is an excellent, fast, and very usable application that I've used numerous times. Its creators deserve significant kudos for releasing a commercial app as open source, but their efforts didn't capture the fancy of a substantial developer community (for good and bad). Xara Xtreme is not available in the standard Ubuntu repositories, but is available for download from http://www.xaraxtreme.org. Its web site hasn't been updated for a while, so I'm not sure how its development is, but it's a great program!

This list, and others that were discussed at length in this chapter, should help you create and edit almost any type of graphical images or objects on an Ubuntu system. It's quite possible that I've missed some excellent graphics applications for Linux—if you fall in love with some application that isn't mentioned here, please let me know. Inquiring minds want to know!

### Summary

This chapter explored tools for creating and manipulating various types of graphics files on Linux systems. Linux has a great selection of powerful graphics tools that you can use to do real work that is constrained only by your artistic skills. (I am still waiting for a "mental image to graphics file" application, but that's my problem.) GIMP, OpenOffice.Org Draw and Inkscape are all shining examples of how excellent and powerful open source software can be.

The next chapter explores how to work with audio and video on Ubuntu systems, with topics ranging from how to configure sound on your system, how to work with CDs, DVDs, and the alphabet soup of digital audio and video file formats that one finds on the Web today.

558
