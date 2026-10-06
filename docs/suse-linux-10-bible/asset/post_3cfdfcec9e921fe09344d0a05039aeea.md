
# Chapter 18 Setting Up Windows Interoperability with Samba 25

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_569_0.png)

Figure 18-22: Samba packages available in SUSE Linux

The capability to operate with other types of computer systems, especially Windows systems, is one of the greatest strengths of Linux. The Samba client and server applications in this chapter make it easy to integrate Linux systems into any networked Windows file and print server environment. A Samba client makes it easy to access existing Windows resources from your Linux system. A Samba server makes it easy for you to export resources from your SUSE system to the networked Windows environment. Regardless of which way you need to go, or if you need to do both, SU provides great graphical tools for Samba client and server configuration through its YaST system administration utility.

# Setting Up Printing with CUPS

# CHAPTER 19

## In This Chapter

In the early days of Linux, printing was difficult to set up and equally difficult to manage. The print system was known as LPD (line printer daemon). Just as with X configuration, in the early days, at least, grown men wept. I still have bitter memories from 1997 of trying to make sense of the Linux Printing HOWTO and when I thought I had cracked it, ending up with a huge stack of paper covered in apparent garbage (raw PostScript code).

- Setting up local printers with YaST
- Printing to remote printers
- Setting up a print server for the local network
- Setting up clients on Linux or Windows
- Using the CUPS web interface
- Controlling printing with command-line tools
- CUPS logs
- Documentation

Fortunately, those days are gone. The standard now is CUPS (the Common Unix Print System) which implements (among other protocols) IPP (the Internet Printing Protocol). CUPS is also used by Mac OS X and is available for other forms of Unix.

A CUPS server can act as a print server for clients operating systems, including Windows. This means that it is not necessary for a Linux server to run Samba (see Chapter 18) to offer printing services to Windows clients.

On SUSE, as one would expect, the configuration of printing has been integrated into YaST. YaST's printer configuration tool is all you need to set up printing for a single machine and for a print server for a small network. If you need a print server with more complex requirements, then a knowledge of the CUPS configuration files and perhaps also its web interface is useful.

SUSE's default CUPS setup differs only slightly from the standard CUPS defaults. This means that a simple setup for a locally attached printer or a simple network print server using YaST — you don't need to use the CUPS administration.

# Printing in Linux: The Role of PostScript

As we have previously, the essentials of printing in Linux have their origins in the way printing was handled in traditional Unix systems, which originally printed to line printers that were only capable of printing lines of text characters.

The first printers with graphical capabilities used the PostScript language. As a result PostScript became a standard page description language. PostScript was introduced by Adobe Systems and dates back to 1982. It is both a page description language and a printer control language (that is, it describes the layout of the text and graphical elements on the printer and can directly control the printer if the printer uses PostScript as its “native language”). PostScript is actually a full programming language; it is possible to include loops and other programming constructs in PostScript files, which can make the output arbitrarily complicated.

When other printers became common, PostScript was still used for the internal representation of the page on Unix systems: the PostScript file was then sent to the printer through a filter that converted it into the printer's native language.

Printers from different manufacturers use different control languages to describe the pages they are going to. In case of HP printers, this will be one of the versions of PCL (printer control language, which is currently at version 6). Epson printers use a native language called ESC/P. Whatever the “native language” of the printer is, when an application wants to print, the PostScript code the application outputs will need to be converted from PostScript to that native language.

This basic method still applies: normally the Ghostscript program together with the PPD files (PostScript Printer Description files, which describe the capabilities of the printer and how the conversion is to made) provide the method by which the PostScript is transformed into the printer's native language.

PostScript as a format (normally PostScript files have the extension .ps) is widely used in Linux documentation and as a way of exchanging formatted portable files. The programs gv, ghostscript, ggv, and others will display PostScript on the screen. A PostScript file is in fact simply a text file with drawing instructions and text characters in it; if you are curious, view a PostScript file with a pager (such as less) or a text editor.

A full description of PostScript is available in documents known as the BLUE BOOK and the RED BOOK, which are available at www-cdf.fnal.gov/offline/PostScript/BLUEBOOK.PDF and http://partners.adobe.com/public/developer/en/ps/PLRM.pdf.

# Chapter 19 Setting Up Printing with CUPS

## Setting Up a Locally Connected Printer

To begin setting up a printer using YaST, start YaST and from the Hardware menu, select Printer, or from the command line type:

```
yast2 printer
```

You will see the window shown in Figure 19-1.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_573_0.png)

YaST usually detects any directly attached printer (such as parallel or USB printers) immediately. For example, in Figure 19-1 a Laserjet 4L was detected on the parallel port.

If the printer has been correctly detected, continue by selecting Configure. Figure 19-2 shows YaST's suggested configuration.

You will find some options here that you can change. In particular, you can change the name that YaST has chosen for the printer (based on its model—in our example inkjet4l) to something more descriptive (like reception or marketing), and you can change the suggested PPD file that will be used. In general, you should accept the recommendation offered by YaST, but you may be to change the quality of printing, particularly for graphics, by experimenting with the alternative PPD files (see Figure 19-3).

530 Part IV Implementing Network Services in SUSE Linux

![](img/e4e45c9f32e76fb35fabbd21a96f1a11e_574_0.png)

Figure 19-2: YaST's printer module: suggested configuration

![](img/e4e45c9f32e76fb35fabbd21a96f1a11e_574_1.png)

Figure 19-3: Choosing a different PPD file in YaST

# Chapter 19 Setting Up Printing with CUPS

## About CUPS

CUPS (the Common Unix Printing System) is a printing system. Whether or not you are printing to a local or a remote printer using CUPS, you will be using a network printing protocol (typically IPP, around which CUPS is based) to connect to cupsd, the CUPS daemon. By default CUPS offers a network service on port 631. IPP is an extension of HTTP. Hence CUPS configuration files look rather like Apache's configuration files.

CUPS offers an administrative interface over HTTP that can be accessed via a URL, such as http://localhost:631/. (The USE documentation and default settings do not particularly encourage the use of the web interface, and for simple setups you will not need it.)

A CUPS server that is attached to a printer can advertise its presence on the network by putting out broadcasts; the clients that will print will learn about these from broadcasts, and if the server allows them to do, they can print through further configuration.

A CUPS server can also print to remote printers using a variety of protocols, including Windows printer shares and direct printing to a network.

The CUPS project pages are at www.cups.org.

You can now print a test page. If all is well, the printer will now produce a nice page with a SUSE logo at the top, a photograph of a red chameleon and colored test images. If nothing comes out of the printer, check that the cable is properly connected. Particularly in the case of a parallel printer, be sure that the cable is not damaged at either.

In all cases, setting up a local printer is as simple as this. There are two problems that might occur. Your printer might not be listed by YaST, and worse, it might not be supported by all.

## Printers Not Listed by YaST

If the printer is not listed, this does not necessarily mean that it is not going to work. If the printer is not a new one from one of the major vendors as HP or Epson, there's a very good chance that it is a variant of one of the printers that is listed by YaST, but it is a changed changed model that has come on the market recently. The best strategy is to select the closest model that you can find manually. Then try printing a test page and see what happens. In many cases this will work fine. The information about your printer at www.linuxprinting.org may help you with this process.
