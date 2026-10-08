
## Chapter 13: Creating and Publishing Documents

## FIGURE 13-18
Creating a new document from a template

![](img/1a233c34336fbf5a85d6eb785e401709_522_0.png)

## Importing Documents from Other Word Processors

Writer can open documents produced by many other word processors, especially those created by Microsoft Word or Corel Word, or documents stored in the intermediate Rich Text Format (RTF) document type. This is fine if you have only one or two documents that you want to update, but if you are moving all of your to Ubuntu, you may find that you have hundreds of documents that you want to update to Writer format. It's a good thing that Writer provides a wizard for that will not only import all of your documents, but will also import and convert any existing or attached style sheets that it detects.

To batch-import your existing Word (or older OpenOffice.org) documents, do the following:

- Select File Wizards Document Converter to display the dialog shown in Figure 13-19.
- To import Word files and style sheets, select the Microsoft Office radio button and select the "Word Documents" checkbox. To import existing SXW documents from StarOffice or a version of OpenOffice.org prior to 2.0, leave the StarOffice radio button selected. Click Next to proceed. The dialog shown in Figure 13-20 displays.

## Part II: Ubuntu for Desktop Users

## FIGURE 13-19
Specifying the input format when converting documents

![](img/1a233c34336fbf5a85d6eb785e401709_523_0.png)

## FIGURE 13-20
Specifying document and template locations when importing

![](img/1a233c34336fbf5a85d6eb785e401709_523_1.png)

- 3. Specify the directories in which you want the wizard to search for the specified document types and the locations to which converted documents should be saved. You may want to update the location to which converted templates should be saved — I typically use my home directory, and subsequently move the files around manually. Once you've
checked the directory locations, click Next to proceed. A status dialog displays, summarizing the conversions that are about to take place. Click Convert to begin the conversion process. The dialog shown in Figure 13-21 displays as the conversion process progresses.

### FIGURE 13-21
Monitoring the document conversion process

![](img/1a233c34336fbf5a85d6eb785e401709_524_0.png)

- 4. During the conversion process, the Conversion Wizard may display a character code confirmation dialog, asking you to select the character set, font, and language you want. This generally means that the Wizard encountered unknown characters in one of the documents. When the conversion process completes, the Close and Show log file buttons are displayed on the dialog shown in Figure 13-21.

Congratulations — the conversion process is complete! Your converted documents and templates are ready for use in Writer. Before clicking Close, it's a good idea to click the "Show log file" button. The log for the conversion process lists successful conversions and identifies any documents that should be fine-tuned or corrected before they can be used with Writer. This is often the case with Word DOT files, which may contain macros that are not completely compatible with anything other than Microsoft's Visual Basic for Applications (VBA).

## More Information about Writer

As mentioned earlier in this chapter, all OpenOffice. applications provide complete, well-written online help. However, like most online help, this information is reference information, not HOWTO information.

If you are serious about using OpenOffice Writer for all of your documentation needs, the best site that I have seen on the Web for HOWTO information about using Writer is www.tutorialsforoffice.org. This site features great tutorials in PDF and OpenOffice org formats, as well as links to a selection of other sites with useful, hands-on information about using Writer. Check it out — it's worth your time! After you become an OpenOffice wizard, you may want to create a tutorial of your own and contribute it to the site.

## Desktop Publishing with Scribus

The previous sections of this chapter discussed how to create different types of documents on Ubuntu systems using command-line and graphical word processors. These tools provide powerful styles to standardize the appearance of repeated elements in your documents. However, when the presentation and layout of your document are as important as its content, you need a different sort of tool. Word and text processors do not just, formatting and organizing the content page margins, sizes of the print area, and the number of columns that are displayed on each page. To actual, detailed document layout, you need an application that combines word processing capabilities with the layout and detailed formatting capabilities required by the publishing industry—in other words, a desktop publishing package. It's good that the open source folks into that problem, too, and an excellent (and free) desktop publishing package for Linux, named Scribus, is easily installed on your Ubuntu system.

Scribus has been under development for a few years now and is an open source application that is available at no cost for Linux, Apple Mac OS X, and Microsoft Windows systems; it uses the QT graphical interface so that it behaves the same way on all supported systems. The Scribus home page is www.scribus.net — check here for the latest Scribus information.

The basic concept in desktop publishing is the frame, which is conceptually similar to the idea of a paragraph in a word processing system. A frame is the key document element in desktop publishing. Desktop publishing documents are composed of many different frames, which can contain text, graphics, and so on. Dividing documents into these compositional elements makes it easy to move or resize them independently to change the document, their target layout, and so on. Text frames can be linked so that text flows from one frame to another, but they are still separately manageable documents.

The next sections explain how to install Scribus, how to create documents using the templates, and what basic steps are necessary to create new documents with the detailed page layout required by your most demanding publishing work. It is not quite XPress, Adobe InDesign, or Adobe PageMaker, but you can't beat the price, and the quality is quite impressive. You can't import existing InDesign, PageMaker, or Quark files yet, although you can import OpenOffice and other forum formats as a starting point.

## Chapter 13: Creating Publishing Documents

## Installing Scribus

Because not everyone wants a desktop publishing package, Scribus isn't installed by default on Ubuntu desktop systems. The primary package that you need to install in order to use Scribus is the scribus package, but you may also want to install the scribus-doc and scribus-template packages to help you make the most of Scribus. See Chapter 19 for more detailed information on installing applications using a variety of package management systems. Once the installation completes, you're ready to begin working with Scribus! Installing Scribus on your Ubuntu system installs a Scribus menu item on the Office menu that you can use to run the application.

## A Quick Scribus Tutorial

Like OpenOffice Writer and most other publishing-related applications, Scribus comes with a few templates to get started. When you first use a new application, it's often easiest to start with someone else's document and modify it to suit your purposes. Once you get the hang of using the application, you can create your own, as explained in the next section. This section provides a whirlwind tour of the key features of Scribus to get comfortable with the basics.

To start Scribus, select Applications Graphics Scribus (This menu command may also be on the Office menu.) Scribus takes a bit of time to start up as it examines your system's font resources (which are critical to a detailed, layout-oriented application). The first time you start Scribus, you will see a "New Document" dialog, as shown in Figure 13-22.

## FIGURE 13-22
Selecting a document layout for a new document

![](img/1a233c34336fbf5a85d6eb785e401709_526_0.png)
