
(called a “druid”) runs and you are greeted by the first of four configuration screens. You simply enter your name, email address, and location and select your connection type. The settings for your audio and video devices are automatically detected; you can view them by selecting the Preferences item from the Edit menu. Figure 5.16 shows Ekiga in action, ready to dial another user.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_149_0.png)

FIGURE 5.16 Ekiga is surprisingly simple to use. A video source is not necessary; a static picture can be used as well.

When you have Ekiga running, you must register (from within Ekiga) with the server at http://ekiga.net/ to enable conferencing; Ekiga does this automatically for you if you told it to do so during the initial configuration.

You can find an informative FAQ at the Ekiga home page at http://www.Ekiga.org/ that you should read in full before using Ekiga. Also, an excellent article about VoIP is at http://freshmeat.net/articles/view/430/.

### NOTE

If you frequently use VoIP applications such as Ekiga, you will tire of repetitively typing in long IP addresses to make connections. To avoid this hassle, you can use a “gatekeeper”—similar in purpose to a DNS server—to translate names into IP addresses. OpenH323 Gatekeeper is one such popular gatekeeper application. It is not provided with Ubuntu, but you can obtain it from http://www.gnugk.org/.

## Reference

- http://www.novell.com/—The home of Ximian Evolution, the standard email client for Ubuntu.
- http://www.mozilla.com/—The home page for Mozilla Firefox, Thunderbird, and the Mozilla Suite.
- http://www.spreadfirefox.com/—The Firefox advocacy home page is useful for converting those Internet Explorer types.
- http://www.konqueror.org/—The homepage for Konqueror.
- http://www.claws-mail.org/— The homepage for Claws, the email client.
- http://ekiga.net/—Sign up here for a free SIP account for use with Ekiga.

## CHAPTER 6

## Productivity Applications

### IN THIS CHAPTER

- Introducing OpenOffice.org
- Office Suites for Ubuntu
- Productivity Applications Written for Microsoft Windows
- Reference

With the rapid growth of open source software, businesses have directly benefited from developments in office productivity suites. Many businesses already use OpenOffice.org and its commercial counterpart, StarOffice, and they are already enjoying the cost benefits of not having to pay license fees or support costs. Of course, more suites are available than just OpenOffice.org, and in this chapter, we will explore the options available.

### NOTE

OpenOffice.org is not 100% compatible with Microsoft Office. Why is this? Well, Microsoft is notoriously secretive about its proprietary file formats, and the only way that OpenOffice.org could ensure compatibility would be to reverse-engineer each file format, an exercise akin to taking apart a telephone to see how it works. This reverse-engineering could be classed as illegal under U.S. law, which would make OpenOffice.org somewhat of a potential hot-potato if they chose this path. However, OpenOffice.org manages to maintain a very high standard of importing and exporting so you should not experience too many problems.

A productivity suite could be classed as containing two or more applications that could be used for creating documents, presentations, spreadsheets, and databases. Other applications could include email clients, calculators/ formula editors, and even illustration packages. Commonly they are all tied together by a default look and feel, which makes sticking to one particular suite much easier. Because Ubuntu uses OpenOffice.org as its standard office suite, we

will introduce you to Writer and Calc, the two most popular OpenOffice.org components. We will also take a brief look at some of the other Linux-based office suites that are available.

### Working with OpenOffice.org

For the majority of users of productivity suites, OpenOffice.org should fulfill most, if not all, of your requirements. However, the first hurdle you need to get over is not whether it can do what you require of it, but rather whether it can successfully import and export to proprietary Microsoft formats. In the main, OpenOffice.org should import and export with minimal hassle, perhaps getting a bit stuck with some of the more esoteric Microsoft Office formatting. Given that most users do not go much beyond tabs, columns, and tables, this level of compatibility should suffice.

However, you are strongly advised to round up a selection of documents that could potentially fall foul of the import/export filter and test them thoroughly (of course, keeping a backup of the originals!). There is nothing worse than for a system administrator who has deployed a new productivity suite than to suddenly get users complaining that they cannot read their files. This would quickly destroy any benefits felt from the other useful functions within OpenOffice.org, and could even spell the return of proprietary formats and expensive office suites. Many users do not mind switching to OpenOffice.org, largely because the user interface closely resembles that of similar Microsoft applications. This helps to settle users into their environment and should dispel any fears they have over switching. Such similarity makes the transition to OpenOffice.org a lot easier.

Of course, just looking similar to Microsoft applications is not the only direct benefit. OpenOffice.org supports a huge array of file formats, and is capable of exporting to nearly 70 different types of documents. Such a wide variety of file formats means that you should be able to successfully use OpenOffice.org in nearly any environment.

### Introducing OpenOffice.org

OpenOffice.org contains a number of productivity applications for use in creating text documents, preparing spreadsheets, organizing presentations, managing projects, and more. The following components of the OpenOffice.org package are included with Ubuntu:

- Writer—This word processing program enables you to compose, format, and organize text documents. If you are accustomed to using Microsoft Word, the functionality of OpenOffice.org Writer will be familiar to you. You will learn how to get up and running with Writer later on in this chapter.
- Calc—This spreadsheet program enables you to manipulate numbers in a spreadsheet format. Support for all but the most esoteric Microsoft Excel functions means that trading spreadsheets with Excel users should be successful. Calc offers some limited compatibility with Excel macros, but those macros generally have to be rewritten. We walk through setting up a basic spreadsheet with some formulas as well as showing you how to build a basic Data Pilot later on in this chapter.
