
## Understanding DocBook

DocBook is a DTD that is well suited for producing computer software documents in a variety of formats. It was originally created by the OASIS Consortium (www.oasis-open.org) and is now supported by many different commercial and open-source tools.

DocBook’s focus is on marking content, instead of indicating a particular look (that is, font type, size, position, and so on). It includes markup that lets you automate the process of creating indices, figure lists and tables of contents, to name a few. Tools in Red Hat Linux let you output DocBook documents into HTML, PDF, DVI, PostScript, RTF, and other formats.

DocBook is important to the Linux community because many open-source projects are using DocBook to produce documentation. For example, the following is a list of organizations, and related Web sites, that use DocBook to create the documents that describe their software:

- Linux Documentation Project (www.tldp.org/LDP/LDP-Author-Guide)
- GNOME Documentation (developer.gnome.org/projects/gdp/handbook/gdp-handbook)
- KDE Documentation Project (www.kde.org/documentation)
- FreeBSD Documentation Project (www.freebsd.org/docproj)

If you want to contribute to any of the above documentation projects, refer to the Web sites for each organization. In all cases, they publish writers' guides or style guides that describe the DocBook tags that they support for their writing efforts.

## Creating DocBook documents

You can create the documents in any text editor, using tags that are similar in appearance to HTML tags (with beginning and end tags appearing between less-than and greater-than signs). There are also word processing programs that allow you to create DocBook markup.

The following procedure contains an example of a simple DocBook document produced with a plain-text editor and output into HTML using tools that come with Red Hat Linux.

1. Create a directory in your home directory to work in and go to that directory. For example, you could type the following from a Terminal window:

```
$ mkdir $HOME/doctest
$ cd $HOME/doctest
```

2. Open a text editor to hold your DocBook document. For example, you could type:

```
$ kedit cardoc.sgm1
```

3. Enter the tags and text that you want to appear in your document. Most DocBook documents are either `<book>` type (large, multi-chapter documents) or `<article>` type (single chapter documents). To try out a DocBook document, type the following:

```xml
<?xml version="1.0"?>
<article>
    <title>Choosing a new car</title>
    <artheader>
        <abstract>
            In this article, you will learn how to price,
            negotiate for, and purchase an automobile.
        </abstract>
    </artheader>
    <section>
        <title>Getting Started</title>
        <para>
            The first thing you will learn is how to figure out
            what you can afford.
        </para>
    </section>
    <section>
        <title>The Next Step</title>
        <para>
            After you know what you can afford, you can begin your
            search.
        </para>
    </section>
</article>
```

There are a few things you should notice about this document. The entire document is wrapped in article tags (`<article>` `</article>`). The article title is in title tags (`<title>` `</title>`). The section tags (`<section>` `</section>`) indicate sections of text that have a title and paragraph each. These sections can later be treated separately in the TOC.

4. Save the file and exit from the text editor.

5. Next, you can try translating the document you just created into several different formats. For example, to create HTML output you could type the following:

```
$ db2html cardoc.sgm1
```

The result is a new directory called `cardoc`. The result from `db2html` in the `cardoc` directory was: `stylesheet-images` directory, `t2.html` file, and `x12.html` file.

6. To view the HTML file just created, I typed the following:

```
$ epiphany $HOME/doctest/cardoc/t2.html
```

Figure 6-11 shows an example of the output created from the db2html command. The screen on the left shows the first page. Click on the Next link at the top of the page. The second page that you see is shown on the right. During conversion to HTML, the db2html command adds Next/Previous buttons to each page. It also puts the title of each section in a Table of Contents on page one and in the browser's title bar.

![](img/27a85d56d393921ced6412ae6e8336bf_254_0.png)

**Figure 6-11:** The DocBook file is output in HTML with the db2html command.

From this point, you can continue to add content and different types of tags. If you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.

### Converting DocBook documents

The previous example shows how to create a simple DocBook document and convert it to HTML output. The following Red Hat Linux utilities convert DocBook to other formats:

- **docbook2dv** — Converts a DocBook file to Device Independent file format.
- **docbook2html** — Converts a DocBook file to HTML format.
- **docbook2man** — Converts a DocBook file to man page format.
- **docbook2pdf** — Converts a DocBook file to Portable Document Format (PDF).
- **docbook2ps** — Converts a DocBook file to PostScript format.
- **docbook2rtf** — Converts a DocBook file to Rich Text Format (RTF).
- **docbook2tex** — Converts a DocBook file to TeX format.
- **docbook2texi** — Converts a DocBook file to GNU TeXinfo format.
- **docbook2txt** — Converts a DocBook file to a bare text format.

## Printing Documents with Red Hat Linux

Printing in Red Hat Linux is provided by the Common UNIX Printing System (CUPS) service. The LPRng service, which is no longer the default printing service used by Red Hat Linux, still can be obtained from Red Hat FTP sites. Both services, however, let you print using the same base set of printing commands described in this section.

> **CROSS-REFERENCE:** See Chapter 10 for a description of how to use the Alternatives system to choose between LPRng and CUPS as the default print service. For information on configuring local and remote printers for Red Hat Linux, see Chapter 17.

As a non-administrative user, you don't have a lot of control over how the printers are configured. You can, however, check which printers are available to print to, check the status of print queues (documents waiting to print), and remove any of your own queued print jobs.

### Printing to the default printer

When your system administrator (or you) configured printers for your computer, one of those printers was defined as the default printer. If you are not sure which printer is your default, type `redhat-config-printer` and look for the printer with the check by it.

Most graphical word processors, such as StarOffice and OpenOffice, let you choose a printer from those available. Some of the less sophisticated Linux utilities that run from the command line, however, use only the default printer. For example, `dvips` (to print a PostScript file) and `groff -1` (to print a troff/nroff file) automatically send the output to the default printer.

As a regular user, you can override the default printer using the `PRINTER` environment variable. For example, if the default printer on your computer is `lp0` and you want to print regularly to `lp1`, change your default printer by setting the `PRINTER` variable as follows:

```
$ export PRINTER=lp1
```

To have this take effect all the time, you could add this line to one of your shell configuration files (such as `$HOME/.bashrc`, if you use the bash shell).

### Printing from the shell

The `lpr` command is used to print files from the shell. You can use `lpr` to print whether the LPRng or CUPS print service is being used. If you have a file already formatted, use `lpr` to print it. For example, if you have a PostScript output file (file.ps) and you want to print it to your PostScript printer, use the following command line:
