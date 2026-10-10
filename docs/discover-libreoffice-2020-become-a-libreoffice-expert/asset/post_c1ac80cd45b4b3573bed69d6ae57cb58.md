
## GET PRODUCTIVE

### LibreOffice Macros

![](img/e39350c3a7c0d527d71b0e4097a0ba66_60_0.png)

Once you have the script on your machine, you can make it executable with:

```bash
chmod +x aws
```

before moving it to the /usr/bin directory.

The next step is to create a new text file and enter your Access Key ID on the first line and the Secret Access Key on the second line. Now save the file as .awssecret in your home directory and use the aws s3dir command to create a new bucket for use with LibreOffice:

```bash
aws s3dir lookup
```

At this point, you can start working on the backup macro. The macro first obtains the currently active document and checks to see whether it has already been saved. The latter is required to retrieve the path to the document:

```basic
ThisDoc := ThisComponent
If ThisDoc.IsModified = False Then
    MsgBox ("Save the document first!", 16, "Attention!")
    End Sub
End If
```

Next, the macro saves all unsaved changes in the document:

```basic
ThisDoc = ThisComponent
If ThisDoc.IsModified Then
    ThisDoc.StoreAsURL(ThisDoc.URL, Args)
End If
```

To construct a command that uploads the currently opened document, the macro needs to obtain two things: the document's path and name:

```basic
DocPath := ConvertFromURL(ThisDoc.getURL())
FileName := Dir(ThisDoc.getURL(), 0)
```

If you want the macro to open a certain URL in the default browser, you can feed the URL to the shell command in a third parameter:

```basic
Sub Main
Shell ("xdg-open", 1, "http://en.wikipedia.org/")
End Sub
```

With a few simple tweaks, you can turn the code above into a lookup macro (Listing 1). First, you need to add code that obtains the currently selected word (lines 2–3) and then modify the Shell command so it points to Wikipedia's query URL followed by the selected word (line 4).

To assign a keyboard shortcut to the created macro, choose Tools | Macros | Organize Macros | LibreOffice Basic. In the dialog that opens, click the Assign button. A new Customize dialog will pop up (Figure 2).

Click the Keyboard tab and choose a shortcut with an empty slot from the Shortcut Keys section. To find the Lookup function you just wrote, look under LibreOffice Macros in the Category pane at the bottom of the dialog, and then highlight the macro in the Function pane and click the Modify button to assign it.

In the example shown in Figure 2, I assigned Lookup to the Shift + F10 shortcut. Now, every time I press Shift + F10, I can look up the word under the cursor in the currently opened LibreOffice document.

## BACK UP

Amazon S3 [2] offers unlimited storage at unbeatable prices, so it's a perfect service for off-site backup. With the use of a little bit of LibreOffice Basic magic and the aws Perl script, you can seamlessly back up the currently opened document to Amazon S3. Before you start, you must sign up for Amazon S3 and download the latest version of the aws script from the project's GitHub repository [3].

**Listing 1: Word Lookup Macro**

```basic
01 Sub Lookup()
02     ThisDoc := ThisComponent
03     LookupWord := ThisDoc.CurrentController.getViewCursor()
04     Shell ("xdg-open", 1, "http://en.wikipedia.org/wiki/" & LookupWord.String)
05 End Sub
```

Figure 2: Assigning macros to keyboard shortcuts lets you run them whenever you want.

**Listing 2: Amazon S3 Backup Macro**

```basic
01 Sub AmazonS3Backup()
02     Dim Args() As New com.sun.star.beans.PropertyValue
03     ThisDoc = ThisComponent
04     If ThisDoc.hasLocation = False Then
05         MsgBox ("You have to save the document first!", 16, "Attention!")
06         End Sub
07     End If
08     ThisDocURL = ThisDoc.getURL()
09     If ThisDoc.IsModified Then
10         ThisDoc.storeAsURL(ThisDocURL, Args)
11     End If
12     DocPath = ConvertFromURL(ThisDoc.getURL())
13     FileName = Dir(ThisDoc.getURL(), 0)
14     PutCommand = "s3backup/" & FileName & " " & DocPath
15     Shell("aws put ", 1, PutCommand)
16 End Sub
```

To upload a file to Amazon S3, you can use the `aws put` command, which has the format:

```bash
aws put BUCKET_NAME/foo.txt /path/to/foo.txt
```

To construct the command that uploads the current LibreOffice document, the macro simply inserts the obtained DocPath value in a string, which is then passed to the shell routine:

```basic
PutCommand = "s3backup/" & FileName & " " & DocPath
Shell("aws put ", 1, PutCommand)
```

That's all there is to it. You can see the entire macro in all its beauty in Listing 2.

Although the backup macro does the job, a few features can still be improved. For example, the name of the bucket is specified directly in the macro, which makes it less flexible. If you plan to use different buckets for different types of LibreOffice documents, you might want to tweak the macro so it uses the InputBox() routine to display an input box where you enter the name of the target bucket.

```basic
BucketName = InputBox("Enter bucket name", "Bucket name")
PutCommand = BucketName & "/" & Timestamp & "/" & FileName & " " & DocPath
```

**Listing 3: Timestamping a File Name**

```basic
01 Timestamp = Format(Year(Now), "0000") & _
02     Format(Month(Now), "00") & _
03     Format(Day(Now), "00") & "-" & _
04     Format(Hour(Time), "00") & _
05     Format(Minute(Time), "00") & _
06     Format(Second(Time), "00")
07 BucketName = InputBox("Enter bucket name", "Bucket name")
08 PutCommand = BucketName & "/" & Timestamp & "/" & FileName & " " & DocPath
```

If you want to keep multiple backup copies of the current document, you can modify the macro so it attaches a timestamp to the file name (Listing 3). The code generates a timestamp in the yyyyMMdd-HHMMSS format and prefixes it to the file name.

## SHORTENING URLS

Working with long URLs in Writer documents can be a real nuisance. One way to fix this problem is to use shortened URLs. However, instead of manually converting long URLs with their short equivalents, you can write a macro that does this donkey job for us (Listing 4).

**Listing 4: Shortening a URL**

```basic
01 Sub ShortenSelectedURL()
02     ThisDoc = ThisComponent
03     ThisText = ThisDoc.Text
04     SelectedURL = ThisDoc.CurrentController.getViewCursor()
05     LongURL = SelectedURL.String
06     If LongURL = "" Then
07         MsgBox ("Select URL first.", 16, "Error!")
08         End Sub
09     End If
10     FileName = FreeFile
11     Open "http://is.gd/gpi.php?longurl=" & LongURL For Input As #FileName
12     While Not EOF(FileName)
13         Line Input #FileName, SingleLine
14         If SingleLine <> "" Then
15             StringBuffer = SingleLine
16         End If
17     Wend
18     Close FileName
19     ShortURL = StringBuffer
20     ThisText.insertString(SelectedURL, ShortURL, True)
21 End Sub
```

To perform the URL-shortening operation, the macro relies on the is.gd service, which offers a simple HTTP-based API for converting links. The macro first grabs the currently selected text fragment containing a long URL and turns it into a string. A simple conditional statement then checks whether a selection has been made, and it displays an error message and aborts if the selection is empty.

To obtain the shortened URL, returned by the `is.gd` API call, the macro uses a simple trick: It opens a file for input and feeds the obtained result into it. The macro then reads the first line in the file and assigns its value to the `StringBuffer` variable, which is then assigned to the `ShortURL` variable (lines 9–18). Finally, the macro replaces the selected long link with the shortened URL that it obtained.

## MARKDOWN FORMATTING

Markdown is a lightweight format popular with developers and users alike, and it is supported by several Linux text editors. However, what if you use LibreOffice Writer as your preferred writing tool? Although the document processor doesn't support the Markdown format, you can easily create a LibreOffice Basic macro that converts Writer documents to Markdown-formatted text files.

The macro in Listing 5 can handle headings, bold, italics, and URLs. To perform the formatting operation, the macro relies on three functions: The `MarkupHeadingsFunc` function processes headings in the currently opened document, `MarkupTextFunc` searches by text attributes (i.e., *bold* and *italics*) and performs replacements, and `MarkupURLFunc` finds and formats hyperlinks in the document.

The macro itself can be roughly divided into two parts. The first part processes the text body of the document and applies Markdown tags to headings, formatted text, and URLs. The second part obtains the file name and path of the currently processed document and saves it as plain text with the `.md` file extension.

Thanks to its modular structure, you can easily adapt the macro for use with other markup formats: All you have to do is replace the start and end tags in the main part of the macro and adjust the `MarkupURLFunc` function (lines 53–67). For example, if you want the macro to apply HTML formatting, the relevant parts (lines 4-8, 63) of the macro and the function should look like the code in Listing 6.

**Listing 5: Markdown Formatting Macro**

```basic
01 Sub Markdown()
02     Dim Args(0) As New com.sun.star.beans.PropertyValue
03     ThisDoc = ThisComponent
04     MarkupHeadingsFunc("Heading 1", "#", "")
05     MarkupHeadingsFunc("Heading 2", "##", "")
06     MarkupHeadingsFunc("Heading 3", "###", "")
07     MarkupTextFunc("CharWeight", com.sun.star.awt.FontWeight.BOLD, "**&**")
08     MarkupTextFunc("CharPosture", com.sun.star.awt.FontSlant.ITALIC, "*&*#")
09     MarkupURLFunc
10     If (Not GlobalScope.BasicLibraries.IsLibraryLoaded("Tools")) Then
11         GlobalScope.BasicLibraries.LoadLibrary("Tools")
12     End If
13     DocURL = Dir.getDocumentURL()
14     DocDir = DirectoryManager.getNameOfPath(DocURL, "/")
15     FileName = Left(Dir/DocURL, 0), Len(Dir/DocURL, 0))-4
16     Args(0).Name = "FileName"
17     Args(0).Value = "Text"
18     TextFilePath = ConvertToURL(DocDir & "/" & FileName & ".md")
19     ThisDoc.StoreToURL(TextFilePath, Args())
20 End Sub
21
22 Function MarkupHeadingsFunc(StyleName, StartTag, EndTag)
23     ThisDoc = ThisComponent
24     ThisText = ThisDoc.Text
25     ParaEnum = ThisText.createEnumeration()
26     While ParaEnum.hasMoreElements
27         Para = ParaEnum.nextElement
28         PortionEnum = Para.createEnumeration()
29         While PortionEnum.hasMoreElements
30             Portion = PortionEnum.nextElement
31             If Portion.paraStyleName = StyleName then
32                 Portion.String = StartTag + Portion.String + EndTag
33             End if
34         Wend
35     Wend
36 End Function
37
38 Function MarkupTextFunc(SearchAttrName, SearchAttrValue, ReplaceStr)
39     Dim SearchAttributes()
40     As New com.sun.star.beans.PropertyValue
41     ThisDoc = ThisComponent
42     SearchAttributes(0).Name = SearchAttrName
43     ReplaceObj = ThisDoc.createSearchDescriptor()
44     ReplaceObj.SearchRegularExpression = true
45     ReplaceObj.searchAll = false
46     ReplaceObj.SearchAll = true
47     ReplaceObj.SetSearchAttributes(SearchAttributes)
48     ReplaceObj.SearchString = "*"
49     ReplaceObj.ReplaceString = ReplaceStr
50     ThisDoc.replaceAll(ReplaceObj)
51 End Function
52
53 Sub MarkupURLFunc
54     ThisDoc = ThisComponent
55     ThisText = ThisDoc.Text
56     ParaEnum = ThisText.createEnumeration()
57     While ParaEnum.hasMoreElements
58         Para = ParaEnum.nextElement
59         PortionEnum = Para.createEnumeration()
60         While PortionEnum.hasMoreElements
61             Portion = PortionEnum.nextElement
62             If Portion.HyperlinkURL <> "" then
63                 Portion.String = "[" + Portion.String + " (" + Portion.HyperlinkURL + ")"
64             End If
65         Wend
66     Wend
67 End Sub
```
