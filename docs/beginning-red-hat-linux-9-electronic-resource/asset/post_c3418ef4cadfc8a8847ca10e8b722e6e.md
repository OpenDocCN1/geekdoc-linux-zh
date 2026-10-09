
| Package Name | Description |
| :--- | :--- |
| ggv | This is GNOME Ghostview – a user interface for any postscript files created using tools such as Ghostscript. For more on this, see http://www.cs.wisc.edu/~ghost/gv/index.htm |
| mrproject | This is a graphical project management tool. It's similar to Microsoft Project, allowing you to plan project tasks and resources |
| openoffice | This is the OpenOffice.org office suite. As we've already mentioned, it's a set of office productivity applications. |
| xpdf | This is a PDF file viewer for the X Window system. |

You can safely install any (or all) of the remaining packages alongside OpenOffice, simply by selecting the packages you wish to install and clicking the Update button, just as we described in Chapter 4. (You'll need the distribution disks in order to complete the installation.) Thus, you can experiment with these applications at your leisure, choose your favorites, and (if you wish) uninstall the others later on.

> For more on installing and uninstalling packages with the RPM, see Chapter 4.

We'll spend the remainder of this section looking at some of the applications in the OpenOffice suite. It's worth noting that the latest information and downloads for OpenOffice can be found at http://www.openoffice.org. In particular, you'll find that you can run OpenOffice on a number of different platforms, as well as Linux – this site has OpenOffice downloads for a variety of platforms including Linux, Windows, and Mac OS X. You'll also find localized dictionaries, documentation, and support facilities to help you get the most from these applications.

## Starting an OpenOffice Application

As soon as OpenOffice is installed (either by default as part of the operating system installation, or manually by adding the package via the RPM), it is ready for you to use. You can start any of the OpenOffice applications from the Main Menu | Office menu:

In addition to the menu shortcuts, the OpenOffice installation process also places three shortcut icons within the taskbar at the bottom of the screen; these are for the Writer, Impress, and Calc applications respectively. To invoke any of these applications, just click on the icon:

![](img/b852150740856958b10aff9e8c9d2adc_163_0.png)

It is also possible to run the office applications from the command line interface. By default, the executable files are installed into the /usr/bin directory, which is part of the $PATH environment variable. This means that we can run any of these applications simply by typing its name at the command line. For example, the following command starts the OpenCalc application:

```
$ oocalc
```

Here are the commands for some other applications in the OpenOffice suite:

| Executable | Application |
|---|---|
| oocalc | Spreadsheet application |
| oodraw | Drawing application |
| oomath | Mathematical formula composer |
| ooimpress | Presentation application |
| oowriter | Word processor |
| ooffice | The default OpenOffice window, for creating any OpenOffice document |
| oopadmin | For setting up printers for OpenOffice applications |
| oosetup | The OpenOffice set-up application |

## Common Functionality

To begin, let's take a look at some of the elements that are common to all the applications in the OpenOffice suite:

- The **layout** of the main window of each application will be familiar to you if you've ever used applications such as Microsoft Word. The top part of the application displays the **menu toolbar** and a **function toolbar**. Beneath this is the **object toolbar** and the **ruler**, with the main working area below that. The **status toolbar** is at the bottom of the window, and behaves like Microsoft Word's status bar. To the side of the main working area is the **main toolbar**. The diagram below demonstrates these areas as visible within an OpenOffice application:

![](img/b852150740856958b10aff9e8c9d2adc_165_0.png)

- You can choose to hide some of these toolbars via the View | Toolbars menu option. Unlike Microsoft Word, OpenOffice doesn’t allow you to undock the toolbars or move them around the screen. However, we can customize the contents of a toolbar – either by right-clicking on a toolbar and selecting Customize, or by selecting View | Toolbars | Customize… from the menu. The toolbars vary from application to application, although the Function, Object, and Main toolbars are common to all the OpenOffice applications.

- The menu structure also varies from application to application, and therefore it would be impractical to try and explain all the options here. If you’ve used Microsoft Office then you’ll notice some familiar menu options. Even if you’re unfamiliar with MS Office, you’ll find these quite self-explanatory. For example:
    - The File menu allows you to open, save, and close files, and offers such features as printer and page-reviewing options.
    - The Tools menu allows access to tools that are either incorporated into the application or added via plug-ins. In addition, this menu also usually offers the opportunity to configure various application-specific options.
    - The Window menu allows you to switch between different documents that you have open in the application at the same time.
    - The Help menu provides access to the in-built help system (which, incidentally, is extremely comprehensive, and should be the first port of call for any problems or information you require).

## Compatibility with Microsoft Office

One thing that many first-time Linux users worry about is whether their MS Office documents are compatible with OpenOffice. For example, is it possible to:
- Create a document in Microsoft Word, and then edit it using OpenOffice?
- Save a spreadsheet in OpenOffice, and then use it at work within Microsoft Excel?

These are very valid questions, and the answer to both is “Yes!” OpenOffice’s built-in interoperability features allow you to use OpenOffice applications to load and save documents using file formats that are compatible with other applications (such as those in Microsoft Office). The way in which OpenOffice handles features such as object embedding (and other features that are native to Microsoft Office) must also be configured – to ensure their behavior is as you would expect.

You can configure these options by accessing the Options dialog from Tools | Options menu from any OpenOffice application:

![](img/b852150740856958b10aff9e8c9d2adc_166_0.png)

> Not all OpenOffice applications support specific conversion features (those that do are discussed here), but they all support the ability to load and save between different file formats. You can find out more by looking at each application’s documentation.

Of particular interest here are the options found under the Load/Save node on the left of this dialog. We won’t cover all the options here, but we will cover those associated with compatibility with Microsoft Office.

## General Loading and Saving Options

The option of interest here is the default File Format that is used when you save a document. You can see this option at the foot of the General tab:

![](img/b852150740856958b10aff9e8c9d2adc_167_0.png)

It is here that you can select the default format that the application will use whenever you ask it to save your document to disk (say, using File | Save). As you can see from the screenshot above, when you first install OpenOffice this default document type is set to the OpenOffice.org 1.0 format.

If you want to work with Microsoft Office file formats only, then it is here that you should change this default setting. This can be particularly useful if you transfer files between home and work often, and you don’t want to forget to save in the correct format. For example, suppose you use Microsoft Word XP at your place of work, and OpenOffice’s OpenWriter at home. If you regularly create documents at home for use at work, you can configure OpenWriter to save your documents in Microsoft Word 97/2000/XP format by default, so that these documents are compatible with the software at your place of work.

## VBA Options

It is possible that your documents contain code written using Visual Basic for Applications (VBA). OpenOffice applications can handle VBA code in a number of different ways, but support is limited to documents that originated in Microsoft Word 97/2000, Microsoft Excel 97/2000, and Microsoft PowerPoint 97/2000.

OpenOffice supports VBA through the dialog box below:
