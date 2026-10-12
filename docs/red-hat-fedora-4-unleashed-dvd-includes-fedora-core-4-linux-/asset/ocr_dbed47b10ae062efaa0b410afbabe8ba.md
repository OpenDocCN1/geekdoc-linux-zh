TABLE 11.1  Continued

| Name         | Description                                                         |
|--------------|----------------------------------------------------------------------|
| disable      | Controls CUPS printers                                              |
| dvi          | Converts TeX DVI files to specific PCL format                      |
| enable       | Controls CUPS printers                                              |
| encscript    | Converts text files to PostScript                                    |
| escputil     | Epson Stylus inkjet printer utility                                  |
| grolobp      | groff driver for Canon LBP-4 and LBP-8 laser printers              |
| gs           | The Ghostscript interpreter                                          |
| gsobj        | Ghostscript Bubblejet printer drivers                                |
| gsdj         | Ghostscript Deskjet printer drivers                                  |
| lpadmin      | CUPS command-line based printer utility                              |
| lp           | Starts a CUPS print job                                              |
| lpc          | A Berkeley-subset CUPS printer control client                        |
| lpf          | General printer filter                                               |
| lprm         | A Berkeley-compatible CUPS job queue utility                         |
| lpstat       | Displays CUPS print jobs and printer status                          |
| mpage        | PostScript text formatting utility                                   |
| pbm          | Portable bitmap conversion utilities                                 |
| pr           | Text formatting command                                              |
| psmandup     | Duplex printing utility for non-duplex printers                      |
| reject       | Controls CUPS print job destinations                                 |
| setup        | Launches printer configuration tool                                    |
| smbclient    | SMB print spooler                                                    |
| smbprint     | SMB print shell script                                               |
| smbspool     | SMB printer spooler                                                  |
| thinkjettopbm| Portable bitmap to ThinkJet printer conversion utility               |

Most Linux systems use PostScript as the default document format for printing. Fedora uses the gs command along with CUPS to manage local and remote print jobs and the type of data transferred during a print job. The gs command is used to translate the document stream into a format accepted by the destination printer (which most likely uses HPCL).

You can use the Ghostscript interpreter gs to display its built-in printer devices by using the gs interpreter with its --help command-line option like this:

```
# gs --help
```

> NOTE
> 
> Fedora includes graphical clients you can use to view many different types of documents. For example, to display PostScript documents (including compressed PostScript documents) or PostScript images, use the gv client. To display Portable Document Format (PDF) documents, you can use gv or the xpdf client.