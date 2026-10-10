
- Linux Documentation Project (www.tldp.org/LDP/LDP-Author-Guide)
- GNOME Documentation (developer.gnome.org/projects/gdp/handbook/gdp-handbook)
- KDE Documentation Project (www.kde.org/documentation)
- FreeBSD Documentation Project (www.freebsd.org/docproj)

If you want to contribute to any of the preceding documentation projects, refer to the Web sites for each organization. In all cases, they publish writers' guides or style guides that describe the DocBook tags that they support for their writing efforts.

## Creating DocBook documents

You can create the documents in any text editor, using tags that are similar in appearance to HTML tags (with beginning and end tags appearing between less-than and greater-than signs). There are also word processing programs that allow you to create DocBook markup. You can export documents from OpenOffice.org Writer to DocBook format, for example.

The following procedure contains an example of a simple DocBook document produced with a plain-text editor and output into HTML using tools that come with Fedora and RHEL. (You need to have the set of docbooks packages on the DVD installed to do the following procedure.)

1. Create a directory in your home directory to work in and go to that directory. For example, you could type the following from a Terminal window:
    - `mkdir $HOME/doctest`
    - `cd $HOME/doctest`
2. Open a text editor to hold your DocBook document. For example, you could type:
    - `gedit cardoc.sgml`
    - (A text editor such as jedit, which you can get at www.jedit.org, can also be useful for dealing with the long tag names used in DocBook.)
3. Enter the tags and text that you want to appear in your document. Most DocBook documents are either `<book>`-type (large, multichapter documents) or `<article>`-type (single chapter documents). To try out a DocBook document, type the following:
    - `<xml version="1.0">`
    - `<article>`
    - `<title>Choosing a new car</title>`
    - `<articleheader>`
    - `<abstract>`
    - In this article, you will learn how to price,
    - negotiate for, and purchase an automobile.
    - `</abstract>`

    ```xml
    <articleheader>
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

You should notice a few things about this document. The entire document is wrapped in article tags (`<article>`, `</article>`). The article title is in title tags (`<title>`, `</title>`). The section tags (`<section>`, `</section>`) indicate sections of text that have a title and paragraph each. These sections can later be treated separately in the TOC.

4. Save the file and exit from the text editor.
5. Next, you can try translating the document you just created into several different formats. For example, to create HTML output you can type the following:
    - `db2html cardoc.sgml`

The result is a new directory called cardoc. The result from db2html in the cardoc directory was: stylesheet-images directory, t2.html file, and x12.html file.

6. To view the HTML file just created, I typed the following:
    - `firefox $HOME/doctest/cardoc/t2.html`

Figure 6-11 shows an example of the output created from the db2html command. The screen on the left shows the first page. Click the Next link at the top of the page. The second page that you see is shown on the right. During conversion to HTML, the db2html command adds Next/Previous buttons to each page. It also puts the title of each section in a Table of Contents on page one and in the browser’s title bar.

From this point, you can continue to add content and different types of tags. If you are writing documents for a particular project (such as the Linux projects mentioned earlier), you should get information on the particular tags and other style issues they require.

## Chapter 6: Publishing with Fedora and RHEL

![](img/fb202c163797a743c3c6cf236316bc96_310_0.png)

Figure 6-11: The DocBook file is output in HTML with the db2html command.

### Converting DocBook documents

The previous example shows how to create a simple DocBook document and convert it to HTML output. The following Fedora and RHEL utilities convert DocBook to other formats:

- **docbook2dvi** — Converts a DocBook file to Device Independent file format.
- **docbook2html** — Converts a DocBook file to HTML format.
- **docbook2man** — Converts a DocBook file to man page format.
- **docbook2pdf** — Converts a DocBook file to Portable Document Format (PDF).
- **docbook2rtf** — Converts a DocBook file to Rich Text Format (RTF).
- **docbook2tex** — Converts a DocBook file to TeX format.
- **docbook2texi** — Converts a DocBook file to GNU TeXinfo format.
- **docbook2txt** — Converts a DocBook file to a bare text format.

## Printing Documents with Fedora and RHEL

Printing in Red Hat Linux is provided by the Common UNIX Printing System (CUPS) service. The LPRng service, which is no longer included with Fedora or RHEL, still can be obtained from www.lprng.com/downloads.html. Both services, however, let you print using the same basic set of printing commands described in this section.

> **CROSS-REFERENCE:** For information on configuring local and remote printers for Fedora and RHEL, see Chapter 17.

As a non-administrative user, you don’t have a lot of control over how the printers are configured. You can, however, check which printers are available to print to, check the status of print queues (documents waiting to print), and remove any of your own queued print jobs.

### Printing to the default printer

When your system administrator (or you) configured printers for your computer, one of those printers was defined as the default printer. If you are not sure which printer is your default, type `system-config-printer` and look for the printer with the check by it.

Most graphical word processors, such as StarOffice and OpenOffice.org, enable you to choose a printer from those available. Some of the less sophisticated Linux utilities that run from the command line, however, use only the default printer. For example, `dvips` (to print a PostScript file) and `groff -l` (to print a troff/nroff file) automatically send the output to the default printer.

As a regular user, you can override the default printer using the `PRINTER` environment variable. For example, if the default printer on your computer is `lp0` and you want to print regularly to `lp1`, change your default printer by setting the `PRINTER` variable as follows:

```
$ export PRINTER=lp1
```

To have this take effect all the time, you could add this line to one of your shell configuration files (such as `$HOME/.bashrc`, if you use the bash shell).

### Printing from the shell

The `lpr` command is used to print files from the shell. You can use `lpr` to print whether the LPRng or CUPS print service is being used. If you have a file already formatted, use `lpr` to print it. For example, if you have a PostScript output file (`file.ps`) and you want to print it to your PostScript printer, use the following command line:

```
$ lpr file.ps
```

If you want to specify a particular printer (other than the default), add the `-P*printer*` option. For example, to print to the `lp0` printer, you could type the following:

```
$ lpr -Plp0 file.ps
```

If you want to print more than one copy of a document, use the `-#*num*` option, where `num` is replaced by the number of copies you want. For example, to print five copies of a file, use:

```
$ lpr -#5 file.ps
```

The lpr command can also accept standard output for printing. For example, you can print the output of a groff command by piping that output to lpr as follows:

```
$ groff -Tps -man /tmp/chown.l | lpr -Plp0
```

> **TIP**: The enscript command (in the enscript package) is another useful tool for printing plain-text files. It converts the files to PostScript and sends them to a printer or to a specified file.

### Checking the print queues

To check the status of print jobs that have been queued, you can use the lpq command. By itself, lpq prints a listing of jobs that are in the queue for the default printer. For example:

```
$ lpq
hp is ready and printing
Rank Owner Job Files Total Size
active root 3 hosts 1024 bytes
1st root 7 (stdin) 625 bytes
2nd root 8 mem01.ps 12273 bytes
3rd chuck 9 bixes.ps 10880 bytes
```

The output from lpq shows the printer status and the files waiting to be printed. Rank lists the order in which they are in the queue. Owner is the user who queued the job. Job shows the job number. The Files column shows the name of the file or standard input (if the file was piped or directed to lpr). Total Size shows how large each file is in bytes.

You can add options to lpq to print different kinds of information. By adding -Pprinter, you can see the queue for any available printer. You can also add the job number (to see the status of a particular print job) or a user name (to see all queued jobs for a user).

### Removing print jobs

If you have ever printed a large document by mistake, you understand the value of being able to remove a print job from the queue. Likewise, if a printer is going to be down for a while and everyone has already printed their jobs to another printer, it's sometimes nice to be able to clear all the print jobs when the printer comes back online.

Remove print jobs in Fedora or RHEL using lprm. For example, to remove all jobs for the user named bill (assuming you are either bill or the root user), type the following:

```
$ lprm -U bill
```

The root user can remove all print jobs from the queue (although you can expect to have some unhappy users if you do this often). To do this you add a dash (-) to the lprm command line as follows:

```
$ lprm -
```
