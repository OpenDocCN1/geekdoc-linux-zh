
## Using Calculators

You have a choice of three calculators that you can use with Red Hat Linux:

- xcalc, the X calculator that comes with the X Window System
- GNOME calculator
- KDE calculator

All of these calculators are scientific calculators capable of performing typical calculations such as square root and inverse, as well as trigonometric functions such as sine, cosine, and tangent.

### xcalc calculator

The xcalc calculator is styled after Texas Instruments’ TI-30 model. To use the xcalc calculator, type xcalc & in a terminal window. Figure 20-1 shows the resulting calculator. You can use the calculator by clicking the buttons or by entering the numbers on the keyboard.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_253_0.png)

Figure 20-1
The xcalc TI-30-style calculator

If you prefer the Reverse Polish Notation (RPN) of the Hewlett-Packard calculators, you can get a calculator modeled after the HP-10C by typing the xcalc -rpn & command. In RPN, the operands precede the operation. For example, to add 2.25 to 9.95 on an HP-10C calculator, you press the keys in the following order: 2.25 ENTER 9.95 +.

20 Min.
To Go

### GNOME calculator

The GNOME calculator is based on xcalc, but with a nicer user interface. To run the GNOME calculator, select Main Menu ⇨ Programs ⇨ Utilities ⇨ Simple Calculator in the GNOME panel. Figure 20-2 shows the resulting display of the GNOME calculator.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_254_0.png)

Figure 20-2
The GNOME calculator

If you compare Figure 20-2 with Figure 20-1, you see that both xcalc and the GNOME calculator have the same set of buttons — except the buttons look better in the GNOME calculator.

### KDE calculator

KDE also includes a scientific calculator with more features than xcalc and the GNOME calculator. For example, it can perform calculations in hexadecimal, decimal, octal, and binary format. From the KDE desktop, you can start the KDE calculator by selecting K ⇨ Utilities ⇨ Calculator (or Main Menu ⇨ KDE menus ⇨ Utilities ⇨ Calculator from the GNOME Panel).

With the KDE calculator, you can convert a number from one base to another by simply entering the number with one of the buttons selected and then clicking the desired base. For example, to convert the hexadecimal value FF to decimal, click the Hex button and enter FF. Then click the Dec button to see the answer, which should be 255.

## Using the Spelling Checker

The aspell utility is an interactive spelling checker. When you install Red Hat Linux from the companion CD-ROMs, you have the opportunity to install aspell.

Using aspell is simple. You use it to check the spelling of words in a text file. To do so, simply type aspell check filename. To try out aspell, type some notes and save them in a text file named notes.txt. To run the spelling checker on that file, type the following command in a terminal window:

```
aspell check notes.txt
This note describes the *concensus* reached during the August 16 meeting.
1) consensus                6) consensus's
2) con census               7) consensuses
3) con-census               8) consciences
4) condenses                9) condensers
5) concerns                 0) consensual
i) Ignore                   I) Ignore all
r) Replace                  R) Replace all
a) Add                      x) Exit
?
```

After aspell runs, it scans the file named notes.txt until it finds a misspelled word (any word that does not appear in aspell’s dictionary). As the output shows, aspell displays the sentence with the misspelled word (concensus) and highlights that word by enclosing it in a pair of asterisks Below that sentence, aspell lists possible corrections, numbering them sequentially from 1. In this case, the utility lists consensus — the right choice — as the first correction for concensus. The list also includes a few items labeled with a letter that mean specific actions such as ignore the misspelling or accept the misspelled for the rest of the file.

At the end of the list of choices, aspell displays a question mark prompt. You should press one of the numbers or letter from the list shown in aspell’s output to indicate what you want aspell to do.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_255_0.png)

To read the aspell manual, start the Web browser and select File Open Page and click the Choose File button from the Open Page dialog box. Go to the /usr/share/doc directory and look for a directory name that begins with aspell (the complete name depends on the aspell version number). From the man_html subdirectory of that directory open the 1_Introduction.html file.

## Commercially Available Office Applications

Most businesses need office applications: word processors, spreadsheets, and the like. Initially, Linux lacked in this area; but now, Linux users can choose from several commercial office productivity applications such as WordPerfect Office 2000 for Linux (http://linux.corel.com/), Applixware Office (http://www.vistasource.com/), and StarOffice (http://www.sun.com/staroffice/). These products do cost some money, but the cost is usually less than that for Microsoft Office — the leading office application suite for Windows. (Microsoft Office is a collection of several applications: Microsoft Word for word processing; Microsoft Excel for spreadsheets; Microsoft PowerPoint for presentation graphics; and Microsoft Access for databases.)

This book’s companion CD-ROMs do not include any of these commercial office applications for Linux, but the next few sections briefly describe these applications. As you read the descriptions, you can visit each vendor’s Web site for the products.

### WordPerfect Office 2000 for Linux

Corel Corporation’s WordPerfect Office 2000 for Linux is a complete office applications suite that includes WordPerfect 9 for word processing, Quattro Pro 9 for spreadsheets, and Corel Presentations 9 for presentation graphics. The product comes bundled with many more components such as Adobe Acrobat Reader (for PDF files) as well as many clip art images. Corel even bundles a copy of Corel Linux (based on the Debian distribution), but you can also install and use WordPerfect Office 2000 on Red Hat Linux. WordPerfect Office can open, edit, and save files in a number of Microsoft Word and Microsoft Excel formats, as well as WordPerfect formats from other systems. According to Corel, you need about 140MB of hard disk space for a typical installation of WordPerfect Office 2000; the full installation requires about 450MB.

You can learn more about the latest release of WordPerfect Office 2000 for Linux by visiting Corel’s Web site at http://linux.corel.com/. The links at that Web site lead you to more information and to Corel’s online store where you can purchase the product.

### Applixware Office

Applixware Office is another prominent office application suite for all Linux distributions, including Red Hat Linux. In April 2000, Applix, Inc. formed a separate group — VistaSource, Inc. — that focuses solely on Linux applications.

Like other office suites, Applixware Office includes Words for word processing, Spreadsheets for spreadsheets, and Graphics and Presents for presentation graphics. Additionally, it also has Mail (an e-mail interface) and Data (an interactive relational database browsing tool). Applixware Office can also read and write documents in Microsoft Office and Corel WordPerfect formats as well as several other file formats. Although trial versions are not offered, the entire Applixware Office suite is priced below $100 U.S. You can also purchase Words or Spreadsheets separately; each of these costs less than $50 U.S.

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_257_0.png)

You can learn more about Applixware at VistaSource’s Web site (http://www.vistasource.com/).

### StarOffice

StarOffice is another commercial office applications suite, which was created by StarDivision of Hamburg, Germany and recently purchased by Sun Microsystems. StarOffice is a cross-platform solution — you can run StarOffice on Linux, Windows 95/98/NT, Sun Solaris SPARC, Sun Solaris x86, and OS/2. Also, StarOffice is available in several languages: English, French, German, Spanish, Italian, Swedish, Dutch, and Portuguese. StarOffice 5.2 for Linux is provided in the form of a large tar file (a form of archive), which you can download for free.

StarOffice is unique in that it combines all of its components into a common desktop from which you can open new documents, drag-and-drop documents from one application to another, and access the Internet. StarOffice includes the following components:

- StarOffice Writer for word processing (Microsoft Word-compatible)
- StarOffice Calc for spreadsheets (Microsoft Excel-compatible)
- StarOffice Impress for presentations (Microsoft PowerPoint-compatible)
- StarOffice Draw for vector graphics drawing
- StarOffice Base for data management
- StarOffice Schedule for organizing events, tasks, contacts, and projects
