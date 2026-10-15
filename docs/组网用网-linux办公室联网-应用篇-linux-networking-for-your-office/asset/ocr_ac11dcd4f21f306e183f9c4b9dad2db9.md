# Note

These instructions describe setting up a printer in MacOS 8.6, so you may need to adjust them for older or newer versions. In particular, MacOS X will use a radically different design, which is in fact based on UNIX. Chances are that the details of configuring it for printing will differ from what appears here.

You configure the driver as follows:

+   1. Select Apple, Chooser to bring up the Chooser, shown in Figure 17.2.

![](bbox=[0.35, 0.48, 0.8, 0.68])

# FIGURE 17.2

Apple's Chooser lets you mount networked hard disks or configure printers.

+   2. Click on the LaserWriter 8 icon. You should see the names of the printers you've defined in your Linux computer's papd.conf file appear, along with any printers that are shared by other computers or that exist standalone on the AppleTalk network. Figure 17.2 shows several printers that have already been configured. These existing printers have printer or spool icons next to their names. Figure 17.2 also shows one new one, known as nessus.

+   3. Click the name of the printer you want to define, and then click Create. If you've listed in your Linux papd.conf file a PPD file that's also available on the Macintosh, configuration should proceed automatically. You'll see a number of dialog boxes informing you of MacOS's progress in retrieving information about the printer and in setting it up, and then you'll be dropped back to the Chooser. At this point, you should see a new printer icon on your desktop for the new printer, and the Chooser should show an icon next to the printer name.