# METHOD #1

Lynx
DEB: lynx
RPM: lynx
WWW: http://lynx.browser.org/

To send a Web page as an annotated text file, pipe the output of the Lynx Web browser with the -dump option to mail (see Recipe 33.2 [Using Lynx], page 643). Since the output is plain text, you don’t have to encode it before you mail it.

⇒ Here are two ways to use this.

+   - To send a mail to the address reader@example.com with the contents of http://gutenberg.net/etext98/rnmis10.txt, type (all on one line):
+     ```
+     $ lynx -dump http://gutenberg.net/etext98/rnmis10.txt | mail reader@example.com [RET]
+     ```

+   - To send a mail to the address reader@example.com with the contents of http://gutenberg.net/etext98/rnmis10.txt and with a subject of "Some Reminiscences," type (all on one line):
+     ```
+     $ lynx -dump http://gutenberg.net/etext98/rnmis10.txt | mail -s "Some Reminiscences" reader@example.com [RET]
+     ```

# METHOD #2

Wget
DEB: wget
RPM: wget
WWW: http://www.gnu.org/software/wget/wget.html

To send the HTML source of a Web page, use wget to retrieve the source, using the -q option to suppress messages and sending to the standard output by giving "-" as an argument to the -O option; pipe this to mail (see Recipe 33.5 [Getting Files from the Web], page 653).

⇒ Here are two ways to use this.

+   - To send a mail to the address reader@example.com with the contents of http://gutenberg.net/etext98/, type (all on one line):
+     ```
+     $ wget -q -O - http://gutenberg.net/etext98/ | mail reader@example.com [RET]
+     ```