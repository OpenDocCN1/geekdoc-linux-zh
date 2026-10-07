# Office Suites for Red Hat Linux

Open Database Connectivity (OBDC) is provided in StarOffice but lacking in OpenOffice.org because OpenOffice.org does not include a database. However, the database front end is provided. The document that you can obtain at http://www.unixodbc/doc/0MySql.pdf explains in detail how OpenOffice.org can be configured to use the MySQL database which is provided with Red Hat, providing Microsoft Access-like functionality at no cost. For details on installing and configuring MySQL, see Chapter 17.

OpenOffice.org Draw used to create graphics that can be included in OpenOffice.org documents. It is not meant as a replacement for more general graphics applications, but it has enough features to meet most needs.

Two sites provide additional information on the functionality of OpenOffice.org:

+   - http://dict.probits.com/download_dictionary.html—This site provides instructions and files for installing and hyphenation dictionaries, which are not included with OpenOffice.org.
- http://sourceforge.net/projects/oextras/-This site provides templates, macros, and clip art, which are not provided with OpenOffice.org.

OpenOffice.org is a work in progress, but the current release is on a Sun with the version of StarOffice 6.0. You can browse to the OpenOffice.org Web site to get documentation and answer frequently asked questions and offer feedback.

# Working with GNOME Office

Rather than developing an integrated suite of applications from scratch, the GNOME project has brought together an offering of GTK-based applications from different developers to meet general office needs (sidebar). Because Sun plans to integrate OpenOffice.org with GNOME, continued support and development for some of the GNOME Office components may be in doubt.

The GTK Widget Set

In order to make it easier to program GUI applications, small pieces of code are prewritten to describe some graphical functions of the graphical interface; these functions include drop-down lists, radio buttons, Save dialogs, window buttons, and the like. Such functions are referred to as widgets, the collection of widgets is referred to as a tool or a widget set. Rather than write the code for all these functions from scratch, programmers need only reference the widgets. This writing GUI applications is easy. Whereas Windows and Mac programmers have only one set of widgets to work with, Unix and Linux programmers have many sets that are, unfortunately, incompatible with one another. The KDE desktop uses the Qt widget set, Netscape uses the Motif widget set, and GNOME applications use the GTK widget set.

GTK is an acronym for G Tool. The GIMP (the GNU Image Manipulation Program) is a graphics application that is very similar to Adobe Illustrator. By using the jargon GTK-based, we save ourselves hundreds of words of typing and help over our discussion of GNOME Office along. You may also see similar references to QT and Motif, as well as other widget sets, in these chapters.

![](bbox=[0.925, 0.375, 0.977, 0.433])