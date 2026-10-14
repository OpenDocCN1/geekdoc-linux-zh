
## NOTE

The decision by the state of Massachusetts to standardize on PDF and OpenDocument has huge ramifications for the open source world. It is the first time that OpenDocument, an already-agreed open standard, has been specified in this way. What it means is that anyone who wishes to do business with the state government must use OpenDocument-based file formats, and not the proprietary formats in use by Microsoft. Unfortunately for Microsoft, it does not have support for OpenDocument in any of its applications, making them useless to anyone wishing to work with the state government. This is despite Microsoft being a founding member of OASIS, who developed and ratified the OpenDocument standard!

## Working with Gnome Office

The other office suite available for GNOME is Gnome Office, which is a collection of individual applications. Unlike OpenOffice.org, Gnome Office does not have a coherent suite of applications, meaning that you have to get used to using a word processor that offers no integration with a spreadsheet, and that cannot work directly with a presentation package. However, if you need only one or two components, it is worthwhile investigating Gnome Office.

## The GTK Widget Set

Open Source developers are always trying to make it easier for people to build applications and help in development. To this end, there are a number of widgets or toolkits that other developers can use to rapidly create and deploy GUI applications. These widgets control things such as drop-down lists, Save As dialogs, window buttons, and general look and feel. Unfortunately, whereas Windows and Apple developers have to worry about only one set of widgets each, Linux has a plethora of different widgets, including GTK+, QT, and Motif. What is worse is that these widgets are incompatible with one another, making it difficult to easily move a finished application from one widget set to another.

GTK is an acronym for GIMP Tool Kit. The GIMP (The GNU Image Manipulation Program) is a graphics application very similar to Adobe Photoshop. By using the GTK-based jargon, we save ourselves several hundred words of typing and help move along our discussion of GNOME Office. You might also see similar references to QT and Motif, as well as other widget sets, in these chapters.

Here are some of the primary components of the Gnome Office suite that are available in Ubuntu:

- AbiWord—This word processing program enables you to compose, format, and organize text documents and has some compatibility with the Microsoft Word file format. It uses plug-ins (programs that add functionality such as language translation) to enhance its functionality.
- Gnumeric—This spreadsheet program enables you to manipulate numbers in a spreadsheet format. Support for all but the most esoteric Microsoft Excel functions means that users should have little trouble trading spreadsheets with Excel users.
- The GIMP—This graphics application allows you to create images for general use. It can import and export all common graphic file formats. The GIMP is analogous to Adobe’s Photoshop application and is described in Chapter 7, “Multimedia Applications.”
- Evolution—Evolution is a mail client with an interface similar to Microsoft Outlook, providing email, scheduling, and calendaring. It is described in Chapter 5, “On the Internet.”

The loose association of applications known as Gnome Office includes several additional applications that duplicate the functionality of applications already provided by Ubuntu. Those extra GNOME applications are not included in a default installation of Ubuntu to eliminate redundancy. They are all available from the Gnome Office website, at http://www.gnome.org/gnome-office/. Both The GIMP and Evolution are available with Ubuntu by default. You have to use yum or pirut to retrieve the remaining components.

Ubuntu provides the AbiWord editor as part of its Extras, shown in Figure 6.14. AbiWord can import XML, Microsoft Word, RTF, UTF8, plain text, WordPerfect, KWord, and a few other formats. AbiWord is notable for its use of plug-ins, or integrated helper applications, that extend its capabilities. These plug-ins add language translation, HTML editing, a thesaurus, a Linux command shell, and an online dictionary, among other functions and features. If you just need a simple yet powerful word processing application, you should examine AbiWord.

AbiWord is not installed by default in Ubuntu, so you’ll need to install it either using apt-get or synaptic. The package is simply called abiword-gnome, although you might want to install the meta-package gnome-office, which will include the other Gnome Office applications.

After you’ve installed Abiword, it becomes available in the Applications menu, under the Office submenu. Simply click the icon to launch the application.

If you are familiar with Microsoft Works, the AbiWord interface will be familiar to you because its designers based the interface upon Works.

You can use the Gnumeric spreadsheet application to perform financial calculations and to graph data, as shown in Figure 6.15. It can import comma- or tab-separated files, text, or files in the Gnumeric XML format, saving files only as XML or text. You need to install Gnumeric using either apt-get or synaptic in the same way as Abiword. If you have already installed the gnome-office package, Gnumeric will be available under Applications, Office as Gnumeric Spreadsheet.
