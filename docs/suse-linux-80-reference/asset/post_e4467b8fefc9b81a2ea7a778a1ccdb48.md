
```
newbie@earth:~ > gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    -sDEVICE=cr360x360 \
    -dBitsPerPixel=1 -dDithering=gsmono -dNoWeave \
    -sOutputCode=plain \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps \
    quit.ps
```

Here, see the difference in the commands when using a parameter file for the uniprint driver or for another Ghostscript driver. Since all driver-specific parameters are located in the uniprint parameter file, it is not necessary to specify any other driver-specific parameters, unlike other Ghostscript drivers.

## Direct Printer Output

Following each of the commands listed above, the printer-specific data is in `/tmp/out.prn`. These can now be sent straight to the printer with the following root command (without spooler or filter), as long as the printer is connected to the first parallel port `/dev/lp0`:

```
earth: # cat /tmp/out.prn >/dev/lp0
```

## A Little About a2ps

Before printing an ASCII text file with Ghostscript, it must be converted to PostScript, since Ghostscript expects PostScript as input. a2ps (package a2ps) is used for this purpose. a2ps is a powerful tool for producing high-quality PostScript output from simple text. It is a very sophisticated program with numerous command-line options. The most important documentation can be found in the man page for a2ps (man a2ps).

## Examples for Working with a2ps

### Direct Printer Output of a Text File with a2ps

The following command can be used to convert a text file with a2ps to PostScript so two pages are reduced to fit on one:

```
newbie@earth:~ > a2ps -2 --medium=A4dd --output=/tmp/out.ps textfile
```

To examine the output of a2ps in the graphical interface, enter

```
newbie@earth:~ > gs -r60 /tmp/out.ps
```

You may have to scroll the pages in the terminal window where you entered `gs` with `↵`. Exit with `Ctrl` + `C`.

The output of a2ps can be converted to the printer-specific format with

```
newbie@earth:~> gs -q -dNOPAUSE -dSAFER -sOutputFile=/tmp/out.prn \
    {driver-parameter} \
    /tmp/out.ps quit.ps
```

where the `{driver-parameter}` is to be specified as described in the previous section.

The output of Ghostscript can be sent straight to the printer (without spooler or filter) as root with

```
earth:  # cat /tmp/out.prn >/dev/lp0
```

as long as the printer is connected to the first parallel port /dev/lp0.

### Printing Business Cards

To demonstrate all the options a2ps has to offer, we will introduce how to print business cards. Create a business card as a simple text file called

```
Title FirstName LastName
Street
Postal/Zip Code City
E-mail: user@domain
Phone: area-number-extension
```

*File 33: card: A Business Card*

Add the ASCII character `\f` to trigger a formfeed, so each business card is treated as a single page.

```
newbie@earth:~> echo -en "\f" >> card
```

Reproduce this page to ten pieces in a file cards:

```
newbie@earth:~ > for i in $(seq 1 10) ; do cat card >> cards ; done
```

Define the longest line in cards:

```
newbie@earth:~> cat cards | wc -L
```

Convert the file cards to PostScript so that all ten business cards appear in two columns of five, each surrounded by a border, with a maximum width according to the longest line, and without additional headers or footers:

```
newbie@earth:~> a2ps -i -j --medium=a4dj --columns=2 --rows=5 \
    --no-header --chars-per-line=number --output=cards.ps cards
```

Give the command in a single line, disregarding the backslash (`\`) and replacing number with the number shown in the output of the `cat cards | wc -L` command.

After testing the results on the screen by entering `gs -r60 cards.ps` you can print them as described above or with the `lpr` command using the print system (`lpr cards.ps`).

## ASCII Text Encoding

Basic information for encoding ASCII text can be found in the Basics manual in the YaST2, Printers, Manual Configuration chapter. A summary with some additional information follows.

In simple text, every character is encoded as a certain number. The character for each code is defined in the code table. The codes may be displayed differently on the screen and in the printer, depending on which code a particular application uses.

ISO-8859-1 (or Latin 1) is the encoding for Western European languages and ISO-8859-2 (or Latin 2) is the encoding for Central and Eastern European languages. So, in ISO-8859-1, the code 241 (octal) corresponds to a reversed exclamation point, while in ISO-8859-2, a large A with an ogonek. ISO-8859-15 is basically the same as ISO-8859-1 except for code 244 (octal), which produces the Euro symbol.

### Outline

All commands should be entered as a single line, disregarding the backslash (`\`).

Create an ASCII text sample file with

```
newbie@earth:  > echo -en "\rCode 241(octal): \
\241\r\nCode 244(octal): \244\r\f" >example
```

Open three terminal windows in the graphical interface with

```
newbie@earth:  > xterm -fn -*-*-*-*-*-*-14-*-*-*-*-iso8859-1 \
    -title iso8859-1 &
newbie@earth:  > xterm -fn -*-*-*-*-*-*-14-*-*-*-*-iso8859-15 \
    -title iso8859-15 &
newbie@earth:  > xterm -fn -*-*-*-*-*-*-14-*-*-*-*-iso8859-2 \
    -title iso8859-2 &
```

Display each sample file in its own terminal window with

```
newbie@earth: > cat example
```

In the “iso8859-1” display: Code 241 as reversed exclamation point (Spanish)  
Code 244 as a circle with tick mark (general currency symbol)  
In the “iso8859-15” display: Code 241 as reversed exclamation point (Spanish)  
Code 244 as Euro symbol  
In the “iso8859-2” display: Code 241 as large A with tick mark (A with ogonek)  
Code 244 as a circle with tick mark (general currency symbol)

ASCII text is printed according to the encoding configured for each queue (as in the printout of the file example). Printouts of documents produced by text processing systems are not influenced by this encoding.

More information with the proper character display is available: for “iso8859-1” in the man page for iso_8859-1 (man iso_8859-1), for “iso8859-15” in the man page for iso_8859-15 (man iso_8859-15), and for “iso8859-2” in the man page for iso_8859-2 (man iso_8859-2).

## Printing in a TCP/IP Network

### Possible Setups

There are mainly three possibilities for printing in a network:

- The printer in a TCP/IP network is connected locally to one of the hosts (the print server).
- The printer is connected to a “print server unit”, a small device with a TCP/IP network connection.
- The printer has a direct TCP/IP network connection (network printer).

The print jobs are passed through a print filter according to the type of printer model you have.

### Overview: Possible Cases

The main difference is how files to print are filtered. At a certain point in the chain, the output file must be converted to a format the printer can finally print: the printer language (PostScript, HP PCL, ESC/P). This conversion is done by the print filter. With network printers and print server units, the filtering must be done on the client computer, before sending out the print job. If a print server is used, the filtering can be done either on the client or on the print server. The following cases are possible:

**Network printer with filtering on the client:**

1. Client: Converts file to printer data (prefilter)
2. Client: Sends print data to the network printer (forward)

**Print server unit with filtering on the client:**

1. Client: Converts file to print data (prefilter)
2. Client: Sends print data to the print server unit (forward)
3. Print server unit: Sends print data to the printer

**Printer connected to a print server with filtering on the client:**

1. Client: Converts file to print data (prefilter)
2. Client: Sends print data to the print server (forward)
3. Print server: Sends print data to the printer

**Printer connected to a print server with filtering on the print server:**

1. Client: Sends the file to the print server (forward)
2. Print server: Converts the file to print data (filter)
3. Print server: Sends the print data to the printer

Since filtering is managed by the print server, there is no need to configure the client if you are using the LPRng spooler, as LPRng spoolers allow the lpd command to send print jobs directly to remote queues. See more on this in Section *Generating Print Jobs for Remote Queues* on page 206. The LPRng spooler (package lprng) must be installed on the client for this reason, but the spooler itself (the lpd) does not have to be running. Only an empty readable (for all users) file `/etc/printcap` must exist on the client and client users must know the name of the print server and the names of the different queues.
