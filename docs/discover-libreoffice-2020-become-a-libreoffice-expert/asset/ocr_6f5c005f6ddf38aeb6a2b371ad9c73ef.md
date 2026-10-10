# GET PRODUCTIVE

# LibreOffice Macros

![](bbox=[0.08, 0.09, 0.63, 0.48])

Once you have the script on your machine, you can make it executable with

```
```bash
chmod +x aws
```
```

before moving it to the /usr/bin directory.

The next step is to create a new text file and enter your Access Key ID on the first line and the Secret Access Key on the second line. Now save the file as .awssecret in your home directory and use the aws s3dir command to create a new bucket for use with LibreOffice:

```
```bash
aws s3dir lookup
```
```

At this point, you can start working on the backup macro. The macro first obtains the currently active document and checks to see whether it has already been saved. The latter is required to retrieve the path to the document:

```
```bash
ThisDoc := ThisComponent
If ThisDoc.IsModified = False Then
    MsgBox ("Save the document first!", 16, "Attention!")
    ) : End
End If
```
```

Next, the macro saves all unsaved changes in the document:

```
```bash
ThisDoc.ThisDoc
If ThisDoc.IsModified Then
    ThisDoc.StoreAsURL (ThisDoc.URL, Args)
End If
```
```

To construct a command that uploads the currently opened document, the macro needs to obtain two things: the document's path and name:

```
```bash
DocPath := 
    ConvertFromURL (ThisDoc.getURL())
FileName := Dir (ThisDoc.getURL(), 0)
```
```

If you want the macro to open a certain URL in the default browser, you can feed the URL to the shell command in a third parameter:

```
```bash
Sub Main
Shell ("xdg-open", 1, "http://en.wikipedia.org/")
End Sub
```
```

With a few simple tweaks, you can turn the code above into a lookup macro (Listing 1). First, you need to add code that obtains the currently selected word (lines 2–3) and then modify the Shell command so it points to Wikipedia's query URL followed by the selected word (line 4).

To assign a keyboard shortcut to the created macro, choose Tools | Macros | Organize Macros | LibreOffice Basic. In the dialog that opens, click the Assign button. A new Customize dialog will pop up (Figure 2).

Click the Keyboard tab and choose a shortcut with an empty slot from the Shortcut Keys section. To find the Lookup function you just wrote, look under LibreOffice Macros in the Category pane at the bottom of the dialog, and then highlight the macro in the Function pane and click the Modify button to assign it.

In the example shown in Figure 2, I assigned Lookup to the Shift + F10 shortcut. Now, every time I press Shift + F10, I can look up the word under the cursor in the currently opened LibreOffice document.

# BACK UP

Amazon S3 [2] offers unlimited storage at unbeatable prices, so it's a perfect service for off-site backup. With the use of a little bit of LibreOffice Basic magic and the aws Perl script, you can seamlessly back up the currently opened document to Amazon S3. Before you start, you must sign up for Amazon S3 and download the latest version of the aws script from the project's GitHub repository [3].

```
```bash
01 Sub Lookup()
02     ThisDoc := ThisComponent
03     LookupWord := ThisDoc.CurrentController. getViewCursor()
04     Shell ("xdg-open", 1, "http://en.wikipedia.org/wiki/" & LookupWord.String)
05 End Sub
```
```

Figure 2: Assigning macros to keyboard shortcuts lets you run them whenever you want.

# Listing 1: Word Lookup Macro