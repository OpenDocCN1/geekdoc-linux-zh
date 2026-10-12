all of these tasks with the tools provided with Fedora (and a digital image from a digital camera or from a scanner).

This section of the chapter discusses The GIMP, a powerful graphics manipulation tool. (You learned about the other graphics tools that Fedora provides in Chapter 9.) In this section of the chapter, you also learn about graphic file formats supported by Fedora, as well as some tools you can use to convert them if the application you want to use requires a different format.

# The GNU Image Manipulation Program

One of the best graphics clients is The GIMP. The GIMP is a free, GPLed image editor with sophisticated capabilities that can import and export more than 30 different graphics formats, including files created with Adobe Photoshop. It is often compared with Photoshop, and The GIMP represents one of the GNU Projects’ first significant successes. You will see many images in Linux that have been prepared with The GIMP.

The GIMP can be started by clicking a desktop panel menu item or by using the command line, like this:

```
$ gimp &
```

You will see an installation dialog box when The GIMP is started for the first time, and then a series of dialog boxes that display information regarding the creation and contents of a local GIMP directory. This directory can contain personal settings, preferences, external application resource files, temporary files, and symbolic links to external software tools used by the editor.

![](bbox=[0.06, 0.57, 0.9, 0.8])

Although The GIMP is powerful, it does lack two features Adobe Photoshop offers that are important to some graphics professionals.

The first of these is the ability to generate color separations for commercial press printers (CMYK for the cyan, magenta, yellow, key, or black colors). The GIMP uses RGB (red, green, and blue) which is great for video display, not so great for printing presses. The second feature GIMP lacks is the use of Pantone colors (a patented color specification) to ensure accurate color matching.

If these features are important to you, The GIMP is an excellent tool. If you must use Adobe Photoshop, the current version of CodeWeaver’s Crossover Office will run Photoshop in Linux.

These deficiencies might not last long. A CMYK plugin is in the works, and the Pantone issues will likely be addressed in the near future as well.

After the initial configuration has finished, The GIMP’s main windows and toolboxes appear. The GIMP’s main window contains tools used for selection, drawing, movement, view enlargement or reduction, airbrushing, painting, smudging, copying, filling, and color selection. Depending on the version installed on your system, the toolbox can host more than 25 different tools.