
## GET PRODUCTIVE
### LibreOffice Macros

#### BASE DATABASES

The Base application lets you build rather advanced databases for storing all kinds of data, and LibreOffice Basic macros can help you integrate databases with other LibreOffice applications. To see how this works in practice, I'll create a simple Base database for storing text snippets and then create a macro that saves text selections from the current Writer document in the database.

The first order of business is to create a Base database that has a single snippets table comprising two fields: *id* (an INTEGER field that acts as the primary key), and *snippet* (a VARCHAR text field for storing text snippets). When creating the database, tick the Yes, register the database for me check-box to register the database as a data source in LibreOffice. Once the database is ready to go, you can start working on the macro (Listing 7).

To establish a connection to the database, the macro uses the ConnectToDatabase function (line 5). This approach is more flexible because it allows you to establish a connection from any other macro when needed. The function (lines 16-30) includes a simple error-handling mechanism (line 19) that aborts the macro and displays an error message when the macro fails to establish a connection to the database (lines 28-29).

The macro itself performs several actions. First, it initializes the current document and obtains the selection. It then establishes a connection to the database registered in LibreOffice under the snippets name. Next, the macro uses the Join() and Split() routines to sanitize the text selection by properly escaping the single quote (') characters, which is necessary to produce valid SQL queries. The macro then constructs a SQL query that inserts the text snippet into the snippets table.

#### LISTING 6: HTML Formatting

```
...  
04 MarkupHeadingsFunc("Heading 1", "<H1>", "</H1>")  
05 MarkupHeadingsFunc("Heading 2", "<H2>", "</H2>")  
06 MarkupHeadingsFunc("Heading 3", "<H3>", "</H3>")  
07 MarkupTextFunc("CharWeight", com.sun.star.awt.FontWeight.BOLD, "<B>","</B>")  
08 MarkupTextFunc("CharPosture", com.sun.star.awt.FontStyle.ITALIC, "<I>","</I>")  
...  
63 Portion.String = "<A HREF="""" + Portion.HyperlinkURL +"""""" +  
                   Portion.String +"</A>"  
...
```

#### LISTING 7: Database Table Macro

```
01 Sub InsertSnippet()  
02 Dim Library As Object  
03 ThisDoc=ThisComponent  
04 TextSnippet=ThisDoc.getCurrentController().getSelection().getByIndex(0).getString()  
05 Database=ConnectToDatabase("snippets")  
06 TextSnippetSanitized = Join(Split(TextSnippet, "'"," ''),"""")  
07 SQLQuery="INSERT INTO "snippets" " + "("snippet") VALUES "  
08 + "("'" + TextSnippetSanitized + "')"  
09 SQLStatement=Database.createStatement()  
10 Result=SQLStatement.executeQuery (SQLQuery)  
11 Database.close  
12 Database.dispose()  
13 MsgBox ("Text snippet has been saved.",64,"Result")  
14 End Sub  
15  
16 Function ConnectToDatabase(DBName As String) As Object  
17 Dim DatabaseOpt() as new com.sun.star.beans.PropertyValue  
18 DBContext=createUnoService("com.sun.star.sdb.DatabaseContext")  
19 On Error GoTo ErrEnd1:  
20 DataSource=DBCttext.getByName (DBName)  
21 ConnectToDatabase=DataSource.getConnection ("","")  
22 DatabaseFile = DataSource.DatabaseDocument  
23 DatabasePath = DatabaseFile.URL  
24 DatabaseOpt(0).Name = "Hidden"  
25 DatabaseOpt(0).Value = True  
26 DatabaseFile = StarDesktop.loadComponentFromURL(DatabasePath, "_blank",0, DatabaseOpt())  
27 Exit Function  
28 ErrEnd1:  
29 MsgBox("Failed to establish a database connection.",16, "Error"):End  
30 End Function
```

### FINAL WORD

These examples are just a few of the things that you can do using LibreOffice Basic. Even these relatively simple macros can have several building blocks you can easily reuse in your own scripts. Of course, the coding fun doesn't have to stop here. Although LibreOffice Basic is not as flexible and powerful as many other popular programming languages, it can handle practically any LibreOffice-related task you throw at it. So once you've mastered its basics, you can unleash the full potential of the LibreOffice productivity suite.

### INFO

- [1] **LibreOffice Shell function:** https://help.libreoffice.org/7.0/en-US/text/basic/shared/03130500.html
- [2] **Amazon S3:** https://aws.amazon.com/s3/
- [3] **AWS Perl script on GitHub:** https://github.com/timkay/aws

## CLEAR OFF YOUR BOOKSHELF WITH DIGITAL ARCHIVES

Complete your collection of *Linux Magazine* and *ADMIN Network & Security* with our Digital Archive Bundles.

You get a full year of *issues* in *PDF format* to access at any time from any device.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_64_0.png)

bit.ly/2019-Digital-Archives

## GET PRODUCTIVE
### LibreOffice Typography

### Setting type in LibreOffice Writer

### Typecast

![](img/e39350c3a7c0d527d71b0e4097a0ba66_65_0.png)

LibreOffice Writer is a serviceable desktop publisher with more typography features than most users imagine. *By Bruce Byfield*

Years ago, Elizabeth Mathias, an employee of Sun Microsystems, told me a story about StarOffice, the proprietary program that became OpenOffice.org, and later LibreOffice and Apache OpenOffice. According to Mathias, when the Writer module was first developed several decades ago, its programmers were told they would have to use it to document their work. As a result, they made sure that Writer was not simply a word processor, but a layout program as well – to the benefit of free software users everywhere. In fact, although not complete, Writer’s features are advanced enough that it should hardly be considered a word processor at all.

Admittedly, the features of Writer often go unnoticed. If you format manually, you might be completely unaware of them. Even if you use styles, you might not have noticed them fully. In fact, although not complete, Writer’s features are advanced enough that it should hardly be considered a word processor at all.

However, if you want to enhance your document, the tools are waiting. Take, for example, the tools for setting up a header in a page style (Figure 1). Once a header is turned on, you can simply select *Same content left/right* and *Same content on first page*, and your header is set up.

If you want more control, you can give the header separate margins from the main text (*Left margin* and *Right margin*); adjust the space between the bottom of the heading and the main text, making it fixed (*Spacing*) or variable (*Use dynamic spacing*); or make the height of the header fixed (*Height*) or variable (*Autofit height*) as well.

What’s more, that is just the first tab. Click the *More* button, and you can surround the header with a border or separate it from the main text with a signal line, while setting the *style*, *thickness*, and *color*, as well as the distance between the border or box and the header’s contents. You can even customize a shadow to add a 3D effect, although I wouldn’t recommend that feature unless you want a retro 1990s look (Figure 2).

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_0.png)

And so it goes for every feature available in *Writer*. Page margins, tables, text wraps, tables of contents, and superscript and subscript letters – almost every aspect has as much degree of choice as you can imagine. At times, you might need some ingenuity to get the exact layout you want, but the actual limitations are few. You cannot, for example, create a list style that counts down from 10, but adding one manually is a rare and minor inconvenience at best.

### LINE SPACING, KERNING, AND HYPHENATION

Writer’s *customization tools* include many features found only in layout programs. Like most word processors, *Writer* gives you default spacing between lines that are single or double spaced and work reasonably well for many fonts. However, for many fonts, this default makes the text appear too light or too dark. When that happens, *Writer* gives you the alternative of clicking *Indents & Spacing | Line spacing | Fixed* to adjust the line spacing exactly as a professional publisher would, in increments of one-hundredth of a point, or 1/720th of an inch (Figure 3).

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_1.png)

Better yet, if you want complete control over the adjustments, you can create a character style that uses *Format | Character | Position | Spacing to* tweak the spacing between characters by increments of one-twentieth of a point (i.e., 1/720th of an inch). Perfectionists can even create separate character styles to be used with different letter combinations.

The only trouble is, by the time you finish editing and revising, the hyphenation is no longer the best possible result. Fortunately, if you have a hyphenation dictionary installed for the language you are using, you can click *Tools | Language | Hyphenation* to check a document’s hyphenation, positioning hyphens so they fall exactly where you want them (Figure 6). If a poor hyphenation break remains, you can either insert a break manually by pressing Ctrl + - (dash) or prevent a break by listing a word as never to be hyphenated in *Tools | Options | Language Settings |*

![](img/e39350c3a7c0d527d71b0e4097a0ba66_66_2.png)
