| Tag Function | Start Field | End Field |
| :--- | :--- | :--- |
| Title | `<TITLE>` | `</TITLE>` |
| First-level head | `<H1>` | `</H1>` |
| Paragraph | `<P>` |  |
| Line breaks | `<BR>` |  |
| Preformatted text | `<PRE>` | `</PRE>` |
| Anchor/link | `<A HREF=pathname>` | `</A>` |
| Lists: |  |  |
| Numbered | `<OL>` | `</OL>` |
| Unnumbered | `<UL>` | `</UL>` |
| Entry | `<LI>` | `</LI>` |
| Definition list | `<DL>` | `</DL>` |
| Term entry | `<DT>` | `</DT>` |
| Definition entry | `<DD>` | `</DD>` |
| Image |  |  |
| `<IMG SRC=image-uri>` |  |  |
| Text style: |  |  |
| Bold | `<B>` | `</B>` |
| Italic | `<I>` | `</I>` |
| Typewriter | `<TT>` | `</TT>` |

Table 18-2. Sample HTML Tags

# Example 18-10

```
<HTML>
<TITLE>AIX 5L: Apache HTTP Server test page</TITLE>
<BODY BACKGROUND="/images/bigblue.jpg">
  <H1>test 1</H1>
  <H2>test 2</H2>
  <H3>test 3</H3>
  <IMG SRC=foo.gif> A picture of foo.
  <BR>
  Take a look around but <I>don't stay too long.</I>
  <P>
  <B>Please send</B><A HREF=address.html>money!</A>
  <P>
</BODY>
</HTML>
```