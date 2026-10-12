
# Reference

http://www.ximian.com/—The home of Ximian Evolution, the standard email client for Fedora.

http://www.mozilla.org/—The home page for Mozilla Firefox, Thunderbird, and the Mozilla Suite.

http://www.spreadfirefox.com/—The Firefox advocacy home page is useful for converting those Internet Explorer types.

## CHAPTER 9
### Productivity Applications

With the rapid growth of open source software, particularly in the enterprise, it was inevitable that open source office suites would reach a level of maturity that means they are suitable for deployment in a corporate environment. Thanks to the open-sourcing of Sun's StarOffice, Linux can benefit from a true Microsoft Office style office suite by the name of OpenOffice.org. Many businesses already use OpenOffice.org and its commercial counterpart, StarOffice, and they are already enjoying the cost benefits of not having to pay license fees or support costs. Of course, there are more suites available than just OpenOffice.org and in this chapter we will explore the options available.

Despite what some hacks have found, OpenOffice.org is making real inroads into directly replacing Microsoft Office, thanks to a lot of hard work by Sun and the community at large. Although not 100% compatible with Microsoft binary formats (DOC, XLS, and PPT) OpenOffice.org gets it right nearly every time. Unless you are working with extremely complex documents that involve specialized functions only available with MS Office, you should encounter no problems with OpenOffice.org.

**NOTE**

Why is OpenOffice.org not 100% compatible with Microsoft Office? Well, Microsoft is notoriously secretive about its proprietary file formats and the only way that OpenOffice.org could ensure compatibility would be to reverse-engineer each file format, akin to taking apart a telephone to see how it works. This reverse-engineering could be classed as illegal under U.S. law, which would make OpenOffice.org somewhat of a potential hot-potato if they chose this path. However, OpenOffice.org manages to maintain a very high standard of importing and exporting so you should not expect too many problems.

**IN THIS CHAPTER**

- Office Suites for Fedora
- Productivity Applications Written for Microsoft Windows
- Reference

A productivity suite could be classed as containing two or more applications that could be used for creating documents, presentations, spreadsheets, and databases. Other applications could include email clients, calculators/formula editors, and even illustration packages. Commonly they are all tied together by a default look and feel, which makes sticking to one particular suite much easier. Because Fedora uses OpenOffice.org as its standard office suite, we will introduce you to Writer and Calc, the two most popular OpenOffice.org components. We will also take a brief look at some of the other Linux-based office suites that are available.

**NOTE**

As with most projects, the more active development that has taken place, the bigger the overall project. Fedora is no exception to this and the team at The Fedora Project has been very busy pushing Fedora on a diet—removing packages that are not considered to be essential to Fedora or are duplicated in functionality. This includes some productivity applications, so if you try to find one in Add/Remove Programs and it is not there, try installing it with yum (see Chapter 37, “Advanced yum”).

## Office Suites for Fedora

As we have mentioned earlier, OpenOffice.org is the default application suite for Fedora. However, with all things open source, there are plenty of alternatives should you find that OpenOffice.org does not meet your specific requirements. These include the popular Gnome Office and also KOffice, the default KDE productivity suite. You are more likely to hear more about OpenOffice.org, especially as more and more people wake up to the fact that it is compatible with MS Office file formats. In fact, the state of Massachusetts recently elected to standardize on two file formats for use in government, the Adobe Acrobat PDF format and the OASIS OpenDocument format, both of which are supported natively in OpenOffice.org.

**NOTE**

The decision by the state of Massachusetts to standardize on PDF and OpenDocument has huge ramifications for the open source world. It is the first time that OpenDocument, an already-agreed open standard, has been specified in this way. What it means is that anyone who wishes to do business with the state government must use OpenDocument-based file formats, and not the proprietary formats in use by Microsoft. Unfortunately for Microsoft, it does not have support for OpenDocument in any of its applications, making them useless to anyone wishing to work with the state government. This is despite Microsoft being a founding member of OASIS, who developed and ratified the OpenDocument standard!

## Working with OpenOffice.org

For the majority of users of productivity suites, OpenOffice.org should fulfill most, if not all, of your requirements. However, the first hurdle you need to get over is not whether it can do what you require of it, but rather if it can successfully import and export to proprietary Microsoft formats. In the main, OpenOffice.org should import and export with minimal hassle, perhaps getting a bit stuck with some of the more esoteric Office formatting. Given that most users do not go much beyond tabs, columns, and tables, this level of compatibility should suffice.

However, you are strongly advised to round up a selection of documents that could potentially fall foul of the import/export filter and test them thoroughly (of course, keeping a backup of the originals!). There is nothing worse than for a system administrator who has deployed a new productivity suite to suddenly get users complaining that they cannot read their files. This would quickly destroy any benefits felt from the other useful functions within OpenOffice.org, and could even spell the return of proprietary formats and expensive office suites. Many users do not mind switching to OpenOffice.org, largely because the user interface closely resembles that of similar Microsoft applications. This helps to settle users into their environment and hopefully dispel any fears they have over switching. Such similarity makes the transition to OpenOffice.org a lot easier.

Of course, just looking similar to Microsoft applications is not the only direct benefit. OpenOffice.org supports a huge array of file formats, and is capable of exporting to nearly 70 different types of documents. Such a wide variety of file formats means that you should be able to successfully use OpenOffice.org in nearly any environment.

## What Is in OpenOffice.org?

OpenOffice.org contains a number of productivity applications for use in creating text documents, preparing spreadsheets, organizing presentations, managing projects, and more. The following components of the OpenOffice.org package are included with Fedora:

- **Writer**—This word processing program enables you to compose, format, and organize text documents. If you are accustomed to using Microsoft Word, the functionality of OpenOffice.org Writer will be familiar to you. The presentation of these functions in the application menus is slightly different from Microsoft Word's, however, so you might have to hunt for familiar functions. Spell checking, a thesaurus, macros, styles, and a help facility are built in to Writer and work in a manner consistent with other word processors and applications. You will learn how to get up and running with Writer later on in this chapter.

- **Calc**—This spreadsheet program enables you to manipulate numbers in a spreadsheet format. Support for all but the most esoteric Microsoft Excel functions means that trading spreadsheets with Excel users should be successful. Calc offers some limited compatibility with Excel macros, but those macros generally have to be rewritten. Calc also supports data exchange formats such as the Data Interchange Format and dBASE format. We walk through setting up a basic spreadsheet with

![](img/2045828cf45e5632bf056f9ca99d6755_278_0.png)
