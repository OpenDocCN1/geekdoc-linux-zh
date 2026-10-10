Insert Hyperlink  
Insert List Elements  
Insert Heading  
Insert Logical Styles  
Insert Physical Styles  
    Center (C-c C-p c)  
    Fixed (C-c C-p f)  
Insert Text Elements  
    Bold (C-c C-p b)  
    Italic (C-c C-p i)  
Insert Inline Image  
Insert Tables  
Insert Structural Elements  
    Underline (C-c C-p u)  
    Strikeout (C-c C-p s)  
Insert Font Elements  
Insert Scripta  
Insert Timestamp Delimiter (C-c C-u c)  
Browse URL we good (C-c C-u w)  
Load Bib Buffer in Browser (C-c C-u v)  
Turn on Navtex Menu  
Narrow to ASP (C-c C-u a)  
Narrow to PHP (C-c C-u p)  
Narrow to VBScript (C-c C-u b)  
Narrow to JavaScript (C-c C-u j)  
Use JSP

*Figure 19.2* The *html-helper* Menu

These keybindings are enough to get you off to a good start. You will gradually absorb other keybindings by repeatedly seeing them on the menu.

| M-Enter | Inserts the `<p>` paragraph tag. |
|---|---|
| M-Tab | Completes a particle-typed tag. |
| Ctrl-c Ctrl-l [1-6] | Inserts a header tag `<h1>`\`<h1>`, from 1 (the largest) to 6 (the smallest). |
| Ctrl-c M-h [1-6] | Gian Umberto Lauri's newer version uses this rather than Ctrl-c Ctrl-l [1-6] for headers. |
| Ctrl-c - | Inserts the horizontal rule tag, `<hr>`. |
| Ctrl-c Enter | Inserts a forced line break, `<br>`. |
| Ctrl-c Ctrl-a l | Inserts an HTML link, `<a href="">\<a>`. |
| Ctrl-c Spacebar | Inserts a nonbreaking space, `&nbsp;`. |

Another category of tag helps you insert special characters in the HTML language. What if you wanted to use an angle bracket in an HTML file? If you just typed one in, the HTML interpreter (such as Netscape or Lynx) would think it was part of a tag and would be confused. The ampersand (&) character is also a