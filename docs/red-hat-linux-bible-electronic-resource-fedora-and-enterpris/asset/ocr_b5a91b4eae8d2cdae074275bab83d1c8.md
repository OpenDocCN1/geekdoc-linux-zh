Table 6-1 lists the macros that you can use on your man pages. These macros are described on the man(7) manual page (type **man 7 man** to view that page).

# **Table 6-1: Man Macros**

| Macro | Description |
|---|---|
|.B | Bold |
|.BI | Bold, then *italics* (alternate) |
|.BR | Bold, then roman (alternating) |
|.DT | Set default tabs |
|.HP | Begin a hanging indent |
|.I | *Italics* |
|.IB | *Italics*, then **bold** (alternating) |
|.IP | Begin hanging tag. For options. Long tags use .TP. |
|.IR | *Italics*, then roman (alternating) |
|.LP | Begin paragraph |
|.PD | Set distance between paragraphs |
|.PP | Begin paragraph |
|.RB | Roman, then **bold** (alternating) |
|.RE | End relative indent (after .RS) |
|.RI | Roman, then *italics* (alternating) |
|.RS | Begin relative indent (use .RE to end indent) |
|.SB | Small text, then **bold** (alternating) |
|.SM | Small text. Used to show words in all caps. |
|.SH | Section head |
|.SS | Subheading within a .SH heading. |
|.TH | Title heading. Used once at the beginning of the man page. |
|.TP | Begin a hanging tag. Begins text on next line, not same line as tag. |

# **Creating a letter, memo, or white paper with Groff**

Memorandum macros (which are used with the `-mm` option of Groff) were once popular among UNIX users for producing technical documents, letters, and memos. Although more