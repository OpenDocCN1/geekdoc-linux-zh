
3. Give the remote printer a name in the COAS Name Printer dialog box shown in Figure 9.8. It is a very good idea to give the remote printer a name that both indicates that it is remote and identifies its actual physical location. This is especially true when the “remote” printer is in fact local, but connected over the network.

![](img/df365d352a104b50fea29e59a052de4d_261_0.png)

4. Inform the spooler which remote host controls this printer and what the remote host calls this printer. (See Figure 9.9.)

![](img/df365d352a104b50fea29e59a052de4d_261_1.png)

5. Save, Discard, or Cancel this printer entry from the confirmation screen that appears.

## Printing That First Page over the Network

We are now ready to print that first page over the network. You can use several methods to accomplish this, depending on the type of network protocol you are using and how your network is connected.

If you are trying to print over a LAN using Samba, you can test the configuration of the Samba mount with the following command:

```
# testprns remoteIp
```

where you replace `remoteIp` with the actual name of the remote printer in your `/etc/printcap` file.

You should perform several other Samba tests, which are covered in Chapter 16 on Samba. However, if the preceding test works, then your remote printer will probably work also.

To print on a Samba attached printer, enter the following command:

```
# smbclient //servername/printernane
```

You will be prompted for a password on *servername*, which in some instances must be in capital letters. After this you are off and running with a printer available over the network.

If we are trying to print over the network using TCP/IP, entering the following command should produce some printout on the remote printer:

```
# lpr -P RemotePrinterName /etc/profile
```

This will print the file *etc/profile* (a file that is always present) on the remote printer *RemotePrinterName*.

## Formatted Printing

If you are doing just junk printing, everything we have done so far is just fine, but I guess we could save a few trees by limiting the junk printing we do.

The alternative to junk printing is nonjunk printing (also known as formatted printing). Formatted printing is useful when we have a long printout where we need page numbers (ever played 357 pickup?) or headers and footers. Another instance where the ability to add information to each page of a printout would be beneficial is where we wish to have an eyes-only or confidential notice printed on each page of a printout.

If you are using a word processor, this is often very easy. However, you usually don't print out financial records or customer lists with a word processor.

One very effective solution to these issues is the `pr` command. It is found in many versions of UNIX and provides a plethora of options to meet your every need.

For example, the following command:

```
# pr -h "Public Information" -o 20 < pr --help | lpr
```

will give you a nicely formatted page with "Public Information" at the top (along with time and date) containing the help list for the `pr` command.

A little explanation is in order. The first part of the command to be executed is `pr --help`, which produces the help list for the `pr` command. This text is piped into the `pr` command at the beginning of the line `pr -h "Public Information" -o 20`. Not only will it produce formatted output of the input text with a header containing "Public Information" as well as other standard header information, but it will also give you a left margin of 20 spaces (for notes perhaps). The output of this `pr` command is then piped to the `lpr` spooler.

![](img/df365d352a104b50fea29e59a052de4d_262_0.png)

If you think this is more of a typing test than a tree saver, you are probably right. However, if you just add a +356 between the pr and the -h, this command would be:

`pr +356 -h "Public Information" -o 20 < longprintout.txt | lpr`

This command will truly save trees because you will start the printout with the 356th page of `longprintout.txt`. This page will, of course, have the proper header and page number.

Another command that is very useful for formatting text (and saving trees) is the `groff` command. This command is really a front end to the entire `groff` document formatting system and has extensive capabilities especially if you want to format a document for a specific device.

The version of `groff` that is delivered with Caldera supports the following target devices:

- PostScript Printers
- TeX dvi devices
- Several X11 viewers (at 75 and 100 dpi)
- Typewriter-like devices
- Typewriter-like devices using the ISO Latin-1 Character Set
- PCL5 compatible printers

Yet Another formatting command is `troff`. When you require formatting containing fractional point sizes and numeric expressions as might be contained in a physics or mathematics thesis, `troff` is most useful.

## Using Your Printer with Other Applications

Caldera OpenLinux comes bundled with WordPerfect 8 for Linux, which is covered along with other word processing packages in Chapter 25. In order to set up the printer to work with WordPerfect, select the K-Gear icon in the corner, highlight applications, and click on WordPerfect.

On the WordPerfect logo window, select Program and then Printer Control.

In the Printer Control dialog box shown in Figure 9.10, you can administer WordPerfect printers.

![](img/df365d352a104b50fea29e59a052de4d_264_0.png)

In this dialog box, you can select the destination of any WordPerfect print job and hold that printer so that other applications don't interfere with your printer setup by WordPerfect.

In addition, you can view the current WordPerfect print queue and optionally cancel the print job, move it to another printer, reorder the print jobs, stop a print job, or hold a print job.

You can also check the status of a print job by clicking on the print job and then the Status button.

Caldera OpenLinux also comes bundled with Star Office 5.0. Setting up the printers for this application is handled in the dialog box shown in Figure 9.11.

![](img/df365d352a104b50fea29e59a052de4d_264_1.png)

The defaults for this application will work for most printers right out of the box. As you can see, many options that can improve the performance of Star Office are possible. Those of you who wish to use the faxing capabilities of Star Office under Caldera OpenLinux need to explore some of these options.

To start with, if you highlight the printer and click on the Connect button on the Printer Installation dialog box, the Connect dialog box shown in Figure 9.12 will be displayed on your monitor.

# FIGURE 9.12
The Star Office Printer Connect dialog box.

![](img/df365d352a104b50fea29e59a052de4d_265_0.png)

This dialog box allows you to modify or remove printer queues and to configure fax output from Star Office.

If you select Configure fax, you will be taken to an entry box that allows you to select printing to a file or to a pipe and to enter the specific fax command for use by Star Office. The Star Office documentation will provide you with additional information on the specifics of the fax printing options.

## Useful Print Capability Enhancing Programs (and Where to Find Them)

One of the most useful printing tools gives you the ability to print multiple pages of your documents on a single sheet of paper (saving trees again). This tool is mpag, which is available from:

http://www.userfriendly.net/linux/RPM/turbolinux/1.2/RPMS/mpage-2.4-1.i386.html

Note that archives use the _z suffix to mean _Z; in other words, this file is compressed using compress not gzip. This command not only speeds up printing considerably but also saves trees.

Another useful program is nenscript, which will format an ASCII file, convert it to PostScript, and then allow you to select many options such as print in landscape or portrait mode, with one or two columns, with or without headers. nenscript can be found at:

http://www.im.lcs.mit.edu/magnus/nenscript/

## Some Secrets of the Gurus (Junior Division)

When all else fails, sometimes it is useful to check out Grant Taylor's Linux Printing HOWTO Homepage, which can be found at

http://www.picante.com/~gtaylor/pht/

Another very good site to visit if you are attempting to print from Linux to a Windows 95 sited printer is:

http://home1.pacific.net.sg/~harish/linuxprint.html

And a final site for the gurus (Junior Division) that contains most of the packages you would ever want (including the printing packages) is:

http://www.shopternet.net/publiclibrary/RPM/Groups.html

which has all the packages sorted by function.
