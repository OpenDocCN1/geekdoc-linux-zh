According to The UNIX Environment (see Appendix D [References for Further Interest], page 731), the diction tool that came with the old Writer's Workbench just found the phrases, and a separate command called suggest would output suggestions. In the GNU version that works for Linux systems, both functions have been combined in the single diction command.

In GNU diction, the words or phrases are enclosed in brackets "[like this]." If diction has any suggested replacements, it gives them preceded by a right arrow, "-> like this."

When checking more than just a screenful of text, you'll want to pipe the output to less so that you can peruse it on the screen (see Recipe 9.1 [Perusing Text], page 211), or pipe the output to a file for later examination.

⇒ Here are two ways to use this.

+   - To check the file dissertation for clichés or other misused phrases, type:
+     $ diction dissertation | less [RET]

+   - To check the file dissertation for clichés or other misused phrases, and write the output to a file called dissertation.diction, type:
+     $ diction dissertation > dissertation.diction [RET]

If you don't specify a file name, diction reads text from the standard input until you type <CTRL>-D on a line by itself. This is especially useful when you want to check a single sentence, as in Figure 11-3.

```
$ diction [RET]
Let us ask the question we wish to state. [RET]
(stdin):1: Let us [ask the question -> ask]
[we wish to state -> (cliche, avoid)].
<CTRL>-D
$
```

Figure 11-3. Checking a sentence with diction.

To check the text of a Web page, use lynx with the -dump and -nolist options to output the plain text of a given URL, and pipe this output to diction. (If you expect there to be a lot of output, add another pipe at the end to less so you can peruse it.)

To peruse the URL http://www.westegg.com/cliche/random.cgi with markings for possible wordy and misused phrases, type (all on one line):

```
$ lynx -dump -nolist http://www.westegg.com/cliche/random.cgi | diction | less [RET]
```