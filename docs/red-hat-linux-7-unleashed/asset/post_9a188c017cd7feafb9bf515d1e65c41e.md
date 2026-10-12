
Half of the clients listed in Table 8.3 may be used from the command line of an X11 terminal window, or in the case of the xwd client, from the text-only console command line. The xwd client is used to take a snapshot of a running client or the root display of an X11 session. The output of the xwd command is sent directly to the standard output, so you’ll need to use file redirection or the -out command-line option, along with a filename to save your graphic.

For example, if you’re running X, you can press Ctrl+Alt+F2 to jump to the second virtual console, then use the xwd client to take a snapshot of your current X session like this:

```
# xwd -out shot1.xwd -root -display :0
```

### Note

> Note that you may have to enable access to your X11 session before taking screenshots from the console. You can do this by using the xhost command, followed by an allowed hostname (such as stinky.home.org), or a plus sign (+) to allow any host. Note that for security, afterwards you should rescind access by using the xhost and its minus option (-).

You can also use xwd from the command line of an X11 terminal window like this:

```
# xwd >out.xwd
```

After you press Enter, your cursor will turn into a cross-hair, and you can then click on another window or the root desktop to take a picture. To display your screenshot, you can use the xwd client like this:

```
# xwd <out.xwd
```

After you press Enter, the image will be displayed in a window. Click on the window to end the program.

## Taking Screenshots with the import Command

Another capable client you can use to take pictures of the root display or selected windows is the import command, part of John Crissy’s ImageMagick software package. This command, like xwd, is used from the command line, but features on-the-fly sizing, cropping, and rotation operations, along with graphics conversion. You can also use this command to take screenshots of other computers on your network (as long as you’re properly authorized, perhaps with the xhost command). And, like xwd, you can use the import command from the text-only console while an X11 session is running to take pictures of a root display.

For example, to take a picture of the desktop from the command line of an X11 terminal window, use the `import` command, along with its `-window` option and the `root` keyword, like this:

```bash
# import -window root test.gif
```

This example will take a snapshot of the entire display and save it in GIF format in the file named `test.gif`. If you want to take a rotated snapshot of an X11 session on another computer in your LAN, you can use the `import` command’s `-display` option with the hostname and display number and the `-rotate` option, like this:

```bash
# import -window root -display vaio.home.org:0.0 -rotate -90 display.pcx
```

This example will take a portrait-oriented (90-degree) snapshot of the computer `vaio.home.org`’s X11 session and save it in a PCX graphics file named `display.pcx`. The `import` command has more than 30 different command-line options you can use for varied effects!

## GNOME-Enabled Graphics Clients

The advent of The Gnu Image Manipulation Program (GIMP) with its GTK+ Toolkit and GDK Drawing Kit libraries ushered in the growing popularity of the GNOME software libraries and GNOME-aware window managers for X11. This interest on the part of software developers and users has spurred further development of GNOME clients, including various GNOME software utilities for the GNOME distribution. You’ll find a number of graphics utilities included with GNOME on your Red Hat Linux system.

Some of the graphics utilities (listed in Table 8.4) are aimed at a specific purpose, such as viewing a particular graphics document (such as a fax), creating and editing icons, viewing various images (such as PostScript), converting graphics, or perhaps taking pictures of the desktop or windows during an X11 session.

**TABLE 8.4 GNOME Graphics Clients**

| **Client Name** | **Description** |
| :--- | :--- |
| dia | Diagram editor |
| ee | Displays graphics files |
| gcolorsel | X11 color browser |
| gimp | The Gnu Image Manipulation Program |
| g0view | Image browser, graphics editor launcher |
| gphoto | Digital camera photo editor |

For example, the **gphoto** client will handily download images from a variety of digital cameras, then offer them for display in thumbnail views for editing. Connect your camera to your computer’s serial port, then start the gphoto client from your GNOME desktop panel or the command line of a terminal window like this:

```
# gphoto &
```

After you press Enter, you’ll see the main gphoto dialog, as shown in Figure 8.1.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_257_0.png)

**Figure 8.1**
*The gphoto client works with many different types of digital cameras.*

Click the **Configure** menu, then click the **Select Port-Camera Model** menu item. You’ll see a dialog, as shown in Figure 8.2.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_257_1.png)

**Figure 8.2**
*The gphoto client must be configured for your camera before getting to work.*

Click the drop-down menu to select your camera model, then click to select the proper serial port. When finished, click the **Save** button. To begin, click the thumbnail index icon on the toolbar, and gphoto will issue the proper instructions via the serial port to download images. You can also press Ctrl-l, or use the Camera menu to accomplish the same thing. When finished, you should see something like Figure 8.3.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_258_0.png)

**Figure 8.3**
To pick an image to edit with gphoto, first select a thumbnail image.

## Digital Camera Support

The gphoto client directly supports 112 different digital cameras, but don’t be disappointed if your camera’s exact model is not listed in the gphoto configuration dialog. Pick the first camera, then scroll through the list. As each camera is selected, information about compatible cameras will appear in the dialog. For example, if you select the Toshiba PDR-M1 camera you’ll see that the Toshiba configuration will also support the Fuji DS-7, DX-5, 7, 10 and MX-500, as well as Samsung’s Kenox SSC-350N, and others. For the latest version of gphoto, go to http://www.gphoto.org. You’ll find that gphoto now also supports at least seven Canon, Kodak, and Mustek USB cameras.

Using thumbnails is a faster way to view the contents of your camera’s memory and to pick and choose an image. To download one or more images, click to select the desired thumbnails, then click the Download Selected Images button. When finished, gphoto will display the images in tabbed windows behind its main window, as shown in Figure 8.4. You can then use the various toolbar buttons to rotate, flip, resize, and adjust color balance, brightness, and contrast.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_259_0.png)

**FIGURE 8.4**
The gphoto client is a mini-photo editor, and can be used to organize, edit, and color-balance digital images!

## K Desktop Environment Graphics Clients

Like GNOME, KDE depends on special software libraries for its special features, such as drag-and-drop and inter-client communication. Also like GNOME, KDE developers have created and fine-tuned numerous graphics applications for use with KDE.

Red Hat Linux includes the latest stable version of KDE, along with its host of clients; however, newer (but unstable) versions of KDE include many new graphics productivity clients. You'll find a number of these included on your Red Hat CD-ROM's /preview directory. Again, many of the graphics utilities (listed in Table 8.5) have a specific purpose, such as viewing graphics files or creating and editing icons.

**TABLE 8.5** KDE Graphics Clients

| Client Name | Description |
| :--- | :--- |
| katalog | Image cataloging client |
| kchart | Charts graphic creation client |
| kpaint | Creates, edits graphic images |
| kgostview | Displays PostScript documents |
| kgrapher | KDE port of gnuplot client |
| kiconedit | Icon editor |
| killustrator | Vector-based drawing client |
| klipper | KDE clipboard client |
| kpresenter | Presentation editor |
