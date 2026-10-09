
## Graphics Applications

We won't dwell on this application, but we'll note that the user interface is again easy to use and provides a simpler (if less flexible) alternative to the `cdrecord` option. You simply use the top part of the dialog to locate the files you want to record, drag them across to the bottom part of the dialog (which represents the CD-ROM drive), and select the `Record` option.

![](img/b852150740856958b10aff9e8c9d2adc_199_0.png)

There are numerous graphical applications installed within Red Hat Linux; some exist as part of KDE or GNOME. Others can be found within application suites such as OpenDraw (which is included within OpenOffice), and yet others are standalone applications written for the sole purpose of manipulating images.

In this chapter, we'll concentrate on the applications that are installed by default with Red Hat Linux 9: The GIMP, PDF Viewer, GQView, and OpenDraw. Most of these are contained within the Graphics package group (which you'll find under the Applications category of the RPM), and can be found in the `Main Menu | Graphics` menu.

### The GIMP

The GNU Image Manipulation Program (or GIMP, as it's affectionately known) is a very powerful piece of software used for graphic manipulation and is equally at home as a simple paint program as it is retouching photographic images you may have. It may be extended using the plug-in technology common to a number of Linux applications but may also be enhanced by using the internal scripting interface that allows you to automate tasks.

The GIMP has been released under the GNU General Public license and as such is freely distributed software. It is installed by default within Red Hat Linux 9 and it has a web site at [http://www.gimp.org/](http://www.gimp.org/), where you'll find documentation, support, and downloads.

You can start the application by selecting **Main Menu | Graphics | The GIMP**, or by typing `gimp` at the command line. A variety of configuration and control windows appear when you start the application, and you can control which dialogs are open at any given time by using the **File | Dialogs** menu of the main **GIMP** window (which is the top-left of the three windows shown below):

![](img/b852150740856958b10aff9e8c9d2adc_200_0.png)

As you can see, the GIMP application is a discrete window containing a menu, an icon toolbar, and color information. Each new image is seen in its own separate window (not shown here), which carries its own menu (accessed by right-clicking on the image).

The application is considerably more powerful than Microsoft Paint, and its features are more closely aligned with applications such as Photoshop or Paint Shop Pro. For example, it supports:

- Numerous paint tools
- Support for layers and channels
- Advanced scripting and plug-in capabilities
- Gradient editor and blend tools
- Transformation support such as rotate and scale
- Multiple file formats

The GIMP's features are too numerous to list in detail, and again we will leave you to play with the application. The online documentation (found at [http://www.gimp.org/docs.html](http://www.gimp.org/docs.html)) is very thorough and this can be supplemented by the documentation found at its main web site (at [http://www.gimp.org/](http://www.gimp.org/)). In addition, a large collection of resources, available from the web site, covers patterns, palettes, brushes, gradients, scripts, and fonts, and contains links to other important web sites for The GIMP (such as a plug-in registry at [http://registry.gimp.org/index.jsp](http://registry.gimp.org/index.jsp) and the very useful **GIMP User Group** – or GimpForce – at [http://gug.sunsite.dk/](http://gug.sunsite.dk/)).

### GQView

GQView is a simple application that allows you to view a number of graphical images simultaneously. You start by selecting the directory in which the graphic files exist, and then either selecting the file from the left-hand pane with its image being displayed in the right hand pane or using the Slideshow feature available on the View menu.

To start this application, select **Main Menu | Graphics | More Graphical Applications | GQView Image Viewer** or run `gqview` from the command line. The screenshot below shows the utility being used to display screenshots from the Red Hat Linux installation process that we covered back in Chapter 1:

![](img/b852150740856958b10aff9e8c9d2adc_201_0.png)

### PDF Viewer

The **PDF Viewer** is another simple application, whose functionality is limited to viewing PDF files on-screen. To start the PDF Viewer, select **Main Menu | Graphics | PDF Viewer** or run the `xpdf` application from the command line. To access a file, use the right-hand mouse button and select **Open** from the menu.

From the command line you can view a PDF document, specifying it as the first parameter on the command line. If we wanted to display the file `chapter05.pdf`, we would use the following command:

```bash
$ xpdf chapter05.pdf
```

If you want to convert a document into PDF format, there are a number of ways to achieve this. In essence it involves converting to the postscript file format, and then using a utility to convert to the PDF file format using the **PS2PDF** converter supplied with Ghostscript. For more information, see [http://www.pathcom.com/~kuusra/pdf_idx.htm](http://www.pathcom.com/~kuusra/pdf_idx.htm).

### OpenDraw

The **OpenDraw** application is installed as part of the OpenOffice suite, and is similar to the Microsoft Draw application that is now embedded within Microsoft Word. It allows you to draw diagrams using a variety of 2D- and 3D-objects and shapes, group and color them, and then embed your diagrams into your OpenOffice documents. It also supports the generation of graphs and the manipulation of text within your image.

## System Applications

There are numerous other applications available and installed with Red Hat 9. Half the fun of a new operating system is exploring all these applications. There is much that isn't installed by default, but is available on the Internet as freeware.

In this section of the chapter we'll talk about some of the handy system utilities and bread-and-butter applications that are usually not so exciting but are there to make your life easier. The applications we'll examine here are the file managers, file compression utilities, and emulators.

## A Simple Text Editor

For many users, the way in which tasks are accomplished primarily via GUI-based applications is a big attraction. Unix has always been associated with command line input, and it was not until the X-Windows system provided a GUI front-end that things become easier. One application that lends itself to this method of input is the simple text editor.

Of course, you could use editors such as OpenWriter to edit such documents, but the formatting and functionality provided with applications like OpenWriter is really overkill for configuration files and similar documents. This is where **gedit** is very useful.

The **gedit** application is similar to Notepad or Wordpad in MS Windows, and is an effective text editor with a nice graphical user interface. To launch gedit, choose `Main Menu | Accessories | Text Editor`, or type `gedit` at the command line:

![](img/b852150740856958b10aff9e8c9d2adc_203_0.png)

## A File Management Application

A file manager is a GUI that allows you to manage and navigate the various drive types and directory structures on your system and network. Given the size of hard disks today (60GB is normal), and the capacity of CD-ROM drives, DVD-ROM drives, not to mention your local area network, the ability to quickly navigate and manage the files of such devices is extremely important.

To start you off navigating your file system, Red Hat Linux places a link to your home directory (`/home/<username>`) on your desktop – mine is labeled Mark’s Home. This shortcut fires up the favored file manager of Red Hat Linux 9 – the Nautilus application – and hence allows you to manage your files and file system easily via Nautilus’s graphical user interface.

Alternatively, you can start Nautilus by typing `nautilus` at the command line. For example, to start exploring the `/usr` directory you would type:

```bash
$ nautilus /usr
```

Let’s take a look at the Nautilus GUI:
