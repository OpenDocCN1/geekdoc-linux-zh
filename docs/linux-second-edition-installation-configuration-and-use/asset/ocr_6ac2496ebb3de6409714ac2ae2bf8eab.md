The following table (sorted by source formats) provides an overview of the most important conversion programs available under Linux and shows the pages where these programs are explained:

# Conversion programs

| to/fromdos | ASCII → ASCII (DOS/Linux conversion) | page 503 |
| a2ps | ASCII → PS | page 505 |
| mpage | ASCII → PS | page 506 |
| dvips | DVI → PS | page 507 |
| dvilj | DVI → HP Laserjet format | page 508 |
| xv | graphics conversion | page 515 |
| ee | graphics conversion | page 517 |
| gimp | graphics conversion | page 659 |
| lynx | HTML → ASCII | page 331 |
| html2ps | HTML → PS | page 514 |
| groff | man page → ASCII, DVI or PS | page 511 |
| rman | man page → HTML | page 513 |
| xpcd. hpcdctoppm | PCD → graphics format XY | page 517 |
| pdf2ps | PDF → PS | page 515 |
| gs | PS → various printer formats | page 509 |
| mpage | PS → PS (several pages on one sheet) | page 506 |
| psutils | PS → PS (tools for processing PS files) | page 510 |
| ps2pdf | PDF → PDF | page 515 |
| sgml2xy | SGML → ASCII, info. HTML, TEX | page 513 |
| latex, tex | TEX → DVI | page 587 |
| latex2html | TEX → HTML | page 513 |
| pdflatex | TEX → PDF | page 515 |
| makeinfo | TEXI → info file | page 512 |
| texi2html | TEX → HTML | page 513 |

# Text conversion DOS ↔ Linux (fromdos, todos)

When you try to exchange texts between DOS/Windows and Linux, you will encounter problems: line ends are marked differently (this applies to DOS and Windows), and different character sets are used, which affects foreign language characters (only applies to DOS).

Details in brief: under both DOS and Windows, the end of a line is marked by a combination of carriage return and line feed. Unix and Linux do not require the carriage return character and are happy enough with the line feed. This means that a DOS file, when viewed with a Linux editor, shows a ^M character at each end of line. Conversely, a Linux file viewed in a DOS editor turns into an endless snake of characters, because DOS and some Windows programs (such as the NOTEPAD editor) do not recognize the ends of lines.