
OpenOffice is one of the most powerful and popular open source projects on the Web, and the people who are largely responsible for its existence are the folks at Oracle who were formerly part of Sun Microsystems. Scott McNealy, president of Sun Microsystems, has a long-standing rivalry with Microsoft, so it was not surprising when in 1999 Sun purchased StarDivision, the German vendor of a suite of office software called StarOffice. The purchase of StarOffice was originally seen as a way to leverage Sun’s Java offerings (because StarOffice and OpenOffice are both heavily dependent on Java) and to provide Users with an office suite that could run natively on their workstations.

Sun released the then-current source code for StarOffice into the open source community under the terms of Sun Industry Standards Source License (ISSL). Beginning with release 2.0 of the OpenOffice.org, all of the code is now available under the GNU Lesser General Public License (LGPL). Sun still markets StarOffice, which is both supported and offers capabilities beyond those provided by OpenOffice.org—but that is for us, because StarOffice doesn't run on Ubuntu Linux.

Aside from its power and absence of cost, a truly compelling reason for using OpenOffice.org Writer is its use of the new OpenDocument Format (ODF) standard for storing and exchanging documents (www.oasis-org/committees/tc_home.php?wg_abbrev). Historically, all word processors used their own proprietary formats for storing documents, which made it hard when switching from one word processor to another or when simply trying to exchange documents with friends or coworkers who use a different word processor. The OpenDocument standard is designed to provide a published standard for storing documents in an XML format that can instantly be in any other word processor that supports this format. This may seem like a minor thing, but get back to me after you try to open the WordStar files for your family history, short stories, or other documents that you have written long ago but still want to be able to use.

## Tip

If you are interested in document standards or read news occasionally, you may be aware of the arm-wrestling contest between the ODF and Microsoft’s OOXML (Open XML XML) standards regarding which of these gets to be the open document standard. OOXML “won” this battle, but in my opinion would be foolish to use OOXML. A standard that is more than 5,000 pages long (and not even the Microsoft tools conform to the time of this writing) isn't much of a standard as far as I’m concerned. Use ODF and reject this latest offering from Microsoft. It is one thing that their tools and operating system are bloatware—

To avoid repeating the phrase OpenOffice.org Writer more times than necessary throughout the rest of this section, I'll typically refer to OpenOffice.org as Writer (its name to its friends) or occasionally as owriter (the name of the application that you must type to execute OpenOffice.org Writer from a command-line interface).

## Part II: Ubuntu for Desktop Users

## File Extensions for OpenOffice.org Documents

With the adoption of the OpenDocument format, OpenOffice.org Writer changed the names of its default file extensions to reflect the new formats. The following list shows the file extensions used by different OpenOffice.org versions:

- odm: OpenDocument Master Document
- odt: OpenDocument Document, OpenOffice.org 2.0 and greater
- ott: OpenDocument Template, OpenOffice.org 2.0 and greater
- sxw: Writer Document before OpenOffice.org 2.0
- stw: Writer Master Document before OpenOffice.org 2.0

The most common documents you will see and create are with the .odt and .ott file extensions. However, you may encounter the older .sxw format when exchanging documents with long-time users. SXW files are very interesting because they are actually zipped archives containing XML document files and associated metadata. You must use the Document Converter Wizard to import old-format SXW OpenOffice.org files into the new OpenDocument format, as explained in the section "Importing Documents from Other Word Processors" later in this chapter.

## Installing Files for Writer

Writer is installed by default if you install Ubuntu from a Live CD, or from an Alternate Install CD using the Text Mode installer, or the OEM Mode installer. If you want to add Writer or the entire OpenOffice.org suite to a server system that has a graphical interface, you can install them using any of the package management tools discussed in Chapter 19.

One that differentiates Ubuntu from other Linux distributions is their extreme dedication to the user, especially in terms of internationalization. If you are working in a single language, the correct localization packages for your physical location are installed with your default Ubuntu installation. However, if you are installing Writer for creating documents in multiple languages, you may also want to search for and install the appropriate hyphenation, localization, and thesaurus packages for whatever others you are writing for. You can find these by looking for a string that represents the country code that you are looking for. For example, Figure 13-3 shows the specific German language support packages for OpenOffice.org that have been identified by searching for the string -de in a Package Management tool.

## Chapter 13: Creating and Publishing Documents

## Tip

You can install complete language support for all applications (without translating the GNOME framework itself) by installing the appropriate language support meta-package for your target locale (e.g., language-support-country-de) — these packages have names of the form language-support-country-code and include the dictionaries for the specified locale. To fully translate the GNOME interface and all internationalized applications, select the appropriate language packs of the form language-pack-country-code. Once you've installed multiple dictionaries, and on, you can set the default language for your documents in Open Office applications using the Tools ◇ Options ◇ Language Settings ◇ dropdown menu. You can also set the default language for various portions of your documents using the commands on the Tools ◇ Language menu.

FIGURE 13-3

Sample additional language packages for the OpenOffice.org suite

![](img/1a233c34336fbf5a85d6eb785e401709_508_0.png)

## Taking a Tour of Writer

You can start Writer from the command line by executing the writer command. More conveniently, a menu item for Writer is installed in the Applications ◇ Office menu called “OpenOffice.org Word Processor.” To start Writer from the menus, select this menu item. The application starts, displaying an empty document, as shown in Figure 13-4.

## Part II: Ubuntu for Desktop Users

## FIGURE 13-4

Starting Writer

![](img/1a233c34336fbf5a85d6eb785e401709_509_0.png)

Writer provides excellent online help, as do all the tools in the OpenOffice.org suite, so I won't bore you by walking you through each menu and entry that it contains. However, as a quick overview of the Writer interface, the callouts in Figure 13-4 highlight the following areas:

- Menus: The dropdown menus in Writer are organized much like the menus in Microsoft Word to provide a familiar user experience. Menu items with an arrow at their right edge lead to other, related menus.
- Toolbars: By default, Writer displays the Standard and Formatting toolbars, which provide one-click access to specific commands when you click on the appropriate icon. You can modify the list of icons displayed on a toolbar by clicking on the control for that toolbar, located at the far right. You can display other toolbars or deactivate the default toolbar by selecting toolbars from the View Toolbars submenu.
- Rulers: These rulers display the horizontal and vertical location of the text insertion point in the current document. The gray-out portions of each ruler reflect the page margins used in the current document. You can hide these rules by toggling the View Ruler menu command.
