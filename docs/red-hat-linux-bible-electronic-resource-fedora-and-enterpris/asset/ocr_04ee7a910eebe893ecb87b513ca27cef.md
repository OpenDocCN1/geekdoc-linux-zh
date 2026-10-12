modern word processors with a variety of WYSIWYG templates have made mm outdated, in a pinch mm can still be a quick way to create a typeset-style document in a text environment.

To format and print (to a PostScript printer) a document with mm macros, use the following:

```
$ groff -mm -Tps -l letter.mm
```

The following is a simple example of how to use mm macros to produce a letter:

```
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WE
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe:"
.LT
In reference to our telephone conversation on the 4th, I am calling to
confirm our upcoming appointment on the 18th. I look forward to
discussing the merger. I believe we have a win-win situation here.
.FC "Yours Truly,"
.SG
```

The output of the letter, if you use the `groff` command line mentioned in the paragraph preceding the code example, is shown in Figure 6-5.

![](bbox=[0.04, 0.58, 0.45, 0.85])

The mm macros were often used to produce technical memos. The following is an example of a sign-off sheet that might go at the front of a larger technical memo.

```
.TL
```