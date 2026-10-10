
## 252 Free_BSD: The Complete Reference

> **Tip**
>
> Aside from printer output formats, Ghostscript also supports some common graphics file output formats. These include TIFF (tiff42anc and others), PNG (png16, png256, png16m, and others), JPEG (jpeg), EPS (epswrite), PostScript (pswrite), and PDF (pdfwrite). Although creating PostScript output from PostScript input sounds strange, it can be useful in some cases, such as if your PostScript printer chokes on the original PostScript file due to lack of memory or other problems.

When you type a Ghostscript command like this one, you’ll receive a prompt to press ENTER with each new page; then you’ll need to type `quit` at a prompt to exit from the program. You can eliminate these prompts by adding `-dNOPAUSE -dBATCH` to the command prior to the name of input file. These options can be extremely important if you create a custom filter to handle PostScript files.

Once you create an output file, you can send it to the printer (via `cat` or `lpr`—but `lpr` may not work if you’ve set up a filter). You should be rewarded with reasonable output. If you don’t get output, or if you get page after page of gibberish, you may need to try another driver. If you see no hint of any printer activity, such as blinking lights, you may have to go back and investigate basic printer connectivity issues.

## Setting Up a Smart Filter

Several smart filter packages are available for FreeBSD. These are essentially filters like those in Listing 9-2, but more sophisticated. They can identify many different file types and process the files so that they’ll print on your printer. Most commonly, the filters call common file conversion programs to convert input files into PostScript. From there the filters use Ghostscript to turn the file into a format that your printer can understand. (If you have a PostScript printer, this last step is skipped.) Once configured, printing any supported file type is a matter of feeding the file to it. Two particularly popular smart filter packages are `affsfilter` and `magicfilter`, both of which are available from the Print software section of `sysinstall`. This section describes the configuration of `magicfilter`.

The normal way of using `magicfilter` is rather unusual: You call its configuration file as if it were a program. This technique works because the configuration file is marked as executable and begins with a code that FreeBSD uses to launch `magicfilter` as if it were a shell scripting language. The various `magicfilter` configuration files reside in `/usr/local/libexec/magicfilter`, and they’re named after the Ghostscript drivers upon which they depend. For instance, the filter for the ljjet4 Ghostscript driver is called `Ljet4-filter`. As an example of a `magicfilter` configuration in action, consider Listing 9-3, which is Listing 9-1 modified to use `magicfilter` for a Laserjet 4 or compatible printer. As you can see, the only difference is the addition of the call to the `magicfilter` configuration file.

**Listing 9-3**
**Sample /etc/printcap Entry Using magicfilter**

```text
lp|hp4000:\
:lp=/dev/lp0:\
:br#115200:\
:sd=/var/spool/lpd/hp4000:\
:mx#0:\
:s#:\n::if=/usr/local/libexec/magicfilter/ljet4-filter:
```

![](img/f34d37e3abe9f4517128e54f80ab2616_290_0.png)

If **magicfilter** happens to come with a filter that's appropriate for your printer, printer setup is straightforward—or at least, little worse than setting up a raw text queue. If the **magicfilter** package lacks an appropriate filter for your printer, though, you must create one yourself.

![](img/f34d37e3abe9f4517128e54f80ab2616_290_1.png)

Ghostscript—and hence **magicfilter**—provides drivers for classes of printers. For instance, many laser printers use the same Printer Control Language (PCL) used by various *Hewlett-Packard* models, so you're likely to be able to use the *laserjet*, *ljet2dp*, *ljet3*, *ljet4*, and similar drivers (and their similarly-named **magicfilter** configuration files) for printers sold by *Lexmark*, *Brother*, *Okidata*, and others. Consult the **Linux Printing** web site (http://www.linuxprinting.org/printer-list.cgi) for information on what *Ghostscript* driver works well with your printer.

If you need to create a custom **magicfilter** configuration file, I recommend you begin by copying an existing filter for a similar printer. The most important criterion is that you *not* choose a PostScript file (these begin with *%!* or *%ps*) because these send the PostScript output directly to the printer port without invoking **Ghostscript**. Most of the filter files contain references to **Ghostscript** early on in the files, like this:

```text
# PostScript
0 !\t filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
0 `004!` filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
```

To modify your copied configuration file, you must alter the **Ghostscript** driver name specified by the *-SDEVICE* option. Once again, the **Linux Printing** web site's database can be invaluable in learning what to put there. Many **magicfilter** configurations include lines that enable the filter to recognize files in the printer's native language. This feature enables you to print from the applications that can produce native-specific output. If you use an unrelated printer's filter as a model, you may want to remove these lines. If you want to print printer-specific drivers in applications such as **The GIMP**, you must create new rules for your printer's format, which can be tricky. It's usually easier to print PostScript and use **magicfilter's** normal PostScript handling rules.

You may also want to create variants of existing configuration files even for printers that **magicfilter** supports. For instance, you might want to create configurations to print at differing resolutions (changing the *-r* value in the call to *gs*) and set up multiple print queues, one for each resolution. For instance, you might have *epson360* and *epson720* queues to print to an *Epson inkjet* at 360 and 720 dpi, respectively.

Once you’ve modified your /etc/printcap file to use your new filters, restart lpd. You can then test printing by using lpr to print a variety of files. Try paging through your filter files to learn what file types your filter supports. When you try to print a file that’s not supported by magicfilter, the file should quietly disappear from the queue, preventing a possible spew of paper with gibberish. (The root user will receive an e-mail notification of this rejection, though.) If the file type is supported, it should be processed and you should receive reasonable output.

## Controlling a Printer

If you’ve configured your system as you read this chapter, you should now have a functioning print queue on your FreeBSD system. This section describes how to use this print queue, both as an ordinary user and as the system administrator. Topics include submitting print jobs, checking on jobs in the queue, deleting jobs, reordering jobs, and changing the availability of print queues.

### Submitting Print Jobs

This chapter has already referred to the `lpr` utility, which is FreeBSD’s tool for submitting print jobs to the queue. This tool is important enough that it deserves an extended description. You should also know how applications interact with `lpr` to enable you to print directly from a program, rather than generate a PostScript file and then print it manually with `lpr`.

### Using lpr

The `lpr` program accepts a large number of options, some of which are fairly esoteric. Consult the `lpr` man page for details. A simplified syntax is

```bash
lpr [-P*printer*] [-*num*] [-U *user*] [-hnmrs] [*filename*...]
```

The meanings of these options are:

- `-P*printer*` This option sets the printer queue to be used. It may be the most-used `lpr` option on systems that support multiple printers. The default is the value of the *PRINTER* environment variable or `lp` if that variable doesn’t exist. Some versions of `lpr` require that there be no space between the `-P` and the queue name, but the BSD LPD included with FreeBSD can tolerate a space.
- `-#*num*` This option tells `lpr` to generate *num* copies of the printout. For instance, `lpr -#4 afile.ps` creates four copies of `afile.ps`.
- `-U *user*` FreeBSD tracks who submits print jobs. This option, which is accessible to *root* and *daemon* only, enables you to specify the user associated with a print job.
