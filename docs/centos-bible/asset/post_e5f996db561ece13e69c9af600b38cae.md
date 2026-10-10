
7. **Assign Storage Space** — You can either identify a disk partition or create a virtual disk by identifying a filename and size. In either case, the storage area must be large enough to hold your installed guest operating system. You are asked to set up a network connection.

8. **Host Network** — Identify either a virtual network or shared physical network device to provide network connectivity for your guest operating system. Next allocate memory and CPU.

9. **Allocate Memory** — From the total memory shown on the screen, choose the amount of VM memory to use and the maximum amount to use. At least 256 MB is recommended. Also, choose the number of virtual CPUs to start with (typically not more than the logical CPUs on the host system). You are asked to review your install information.

10. **Start Installation** — If all the information is correct, click Finish to begin the install process.

At this point, you run through the installation process as you normally would for the operating system you selected. Once installation is complete, you can start and shut down the new virtual environment from the Virtual Machine Manager.

## Summary

Between applications written directly for Linux and other UNIX systems, those that have been ported to Linux, and those that can run in emulation, thousands of applications are available to be used with CentOS systems.

To simplify the process of installing and managing your Linux applications, Red Hat developed the RPM Package Management (RPM) format. Using tools developed for RPM, such as the `rpm` command, you can easily install, remove, and perform queries on Linux RPM packages. Tools for finding, downloading, and installing RPM packages include the `yum` utility and the Add/Remove Software window.

Of the types of applications that can run in Linux, those created for the X Window System provide the greatest level of compatibility and flexibility when used in Linux. However, using emulation software, it is possible to run applications intended for DOS, Microsoft Windows, and Macintosh operating systems. In the long run, virtualization software such as Xen and KVM will allow multiple operating systems to run as guests on CentOS. That, in turn, will provide a means for running a variety of applications within those systems on CentOS.

# Chapter 6

# Publishing with CentOS

To survive as a desktop system, an operating system must be able to perform at least one task well: produce documents. It’s no accident that, after Windows, Microsoft Word (which is bundled into Microsoft Office) is the foundation of Microsoft’s success on the desktop. CentOS includes tools for producing documents, manipulating images, scanning, and printing. Almost everything you would expect a publishing system to do, you can do with CentOS.

This chapter describes popular Linux office suites (such as OpenOffice.org) for creating documents, presentations, and spreadsheets. For page layouts, Scribus is an excellent application that can be used to create brochures and pamphlets. For working with images, we cover the GNU Image Manipulation Program (The GIMP). For working with vector graphics, we describe the Inkscape vector graphics editor.

For displaying the content you create, there are several different viewers available for displaying output in PDF and PostScript formats. For example, there is the Evince viewer, which can view both PDF and PostScript files. There is also Ghostview, a dedicated PostScript viewer.

If you want to publish on the Web, there are tools for everything from writing basic HTML documents to making web photo sites to implementing full-blown content management systems. Software that is packaged for Linux to manage your own web sites includes MediaWiki (wiki), WordPress (blogging), Drupal (content management), and Gallery (photo web site).

## IN THIS CHAPTER

- Desktop publishing in Linux
- Trying graphical text editors
- Using OpenOffice.org
- Creating documents with Groff and LaTeX
- Creating DocBook documents
- Displaying documents with Evince
- Doing page layout with Scribus
- Working with graphics
- Making Inkscape vector graphics
- Using scanners driven by SANE
- Publishing on the Web

## Desktop Publishing in Linux

Whether you are writing a letter, a memo, or a book, you usually begin with a word processor. If your computer doesn't have much power, you might start with a simple text editor or a less demanding word processor such as AbiWord. Most Linux users, however, begin with OpenOffice.org Writer. If all you need is to edit a plaintext document, however, you can begin with a simple text editor.

### Using Text Editors and Notepads

Before jumping into more complex word processors, here are a few applications you might want to try out if you just want to write some text quickly:

- **GNOME Text Editor (gedit)** — From the GNOME desktop, select Applications
- **KDE Text Editor (KWrite)** — From the KDE desktop, the KWrite application is the default text editor. KWrite includes many of the same text editing features as gedit, but also has bookmark features and support for multiple language input.
- **Sticky Notes (Tomboy)** — Different note taking applications include KNotes (for KDE) and Tomboy (for GNOME). Tomboy puts a notepad icon in your top panel, from which you can create and manage notes. Create a new note that includes URLs (click to open in a browser) and links to other notes. Spelling is checked as you type. Organize notes in notebooks or do keyword searches to find the note you want.

If you want to move text from your plaintext files or sticky notes to a more formal document, you can copy or cut, then paste the text into one of the word processors described in the next section.

### Using Word Processors

OpenOffice.org is a powerful Open Source office suite available as part of the CentOS distributions. Based on the Sun Microsystems StarOffice productivity suite, OpenOffice.org includes a word processor, spreadsheet, presentation manager, and other personal productivity tools. In many cases, OpenOffice.org can act as a drop-in replacement for Microsoft Office, in both its features and its ability to support files in Word, Excel, PowerPoint, and other Microsoft formats.

Commercial office suites include StarOffice, which contains not only a word processor, but also applications for creating and working with spreadsheets, presentations, and other office-oriented content.

## Using OpenOffice.org

Some have called OpenOffice.org a significant threat to Microsoft's dominance of the desktop market. If a need to work with documents in Microsoft Word format has kept you from using Linux as your desktop computer, OpenOffice.org is a big step toward removing that obstacle.

> **NOTE**
> If you are willing to pay a few dollars, CrossOver Developer from Codeweavers.com lets you install and run different versions of Microsoft Office (97, 2000, XP, 2003, and 2007) from your Linux desktop. See Chapter 5 for further information or check out www.codeweavers.com/products/cxoffice.

CentOS includes the entire OpenOffice.org suite of desktop applications. Based on the StarOffice source code, OpenOffice.org consists of the following office-productivity applications:

- **OpenOffice.org Writer** — A word processing application that can work with documents in file formats from Microsoft Word, StarOffice, and several others. Writer also has a full set of features for using templates, working with fonts, navigating your documents, including images and effects, and generating tables of contents.
- **OpenOffice.org Calc** — A spreadsheet application that lets you incorporate data from Microsoft Excel, StarOffice, Dbase, and several other spreadsheet formats. Some nice features in Calc enable you to create charts, set up database ranges (to easily sort data in an area of a spreadsheet), and use the data pilot tool to arrange data in different points of view.
- **OpenOffice.org Draw** — A drawing application that enables you to create, edit, and align objects, incorporate textures, include textures and colors; and work with layers of objects. It lets you incorporate images, vector graphics, AutoCAD, and a variety of other file formats into your drawings. Then you can save your drawing in the OpenOffice.org Drawing or StarOffice Draw formats.
- **OpenOffice.org Math** — A calculation program that lets you create mathematical formulas.
- **OpenOffice.org Impress** — A presentation application that includes a variety of slide effects. Using Impress, you can create and save presentations in the Microsoft PowerPoint, Draw, and Impress formats.

Unlike other applications that were created to work with Microsoft document and data formats, OpenOffice.org (although not perfect) does a very good job of opening and saving files from many different versions of Microsoft Word (.doc) and Excel (.xls) formats with fewer problems. Very basic styles and formatting that open in OpenOffice.org often don't look noticeably different from the way they appear in Microsoft Office. In fact, some older Word documents will actually work better in OpenOffice.org Writer than they do in the latest Microsoft Office suites.

> **NOTE**
> The Open Office XML (OOXML) format, a 6,000-page tome, represents Microsoft's recent efforts to claim to support standard document formats. This format is the default document type in Word 2007. Some people in the Open Source community, however,
