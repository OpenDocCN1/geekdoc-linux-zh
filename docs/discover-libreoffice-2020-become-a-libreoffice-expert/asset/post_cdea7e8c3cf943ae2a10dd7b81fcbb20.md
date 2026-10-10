
# GET PRODUCTIVE

## Digital Signatures

![](img/e39350c3a7c0d527d71b0e4097a0ba66_71_0.png)

Then create a decrypted copy of the file with:

```
gpg --decrypt ENCRYPTED-FILE
```

The file’s text appears in the command line, and an unencrypted version of the file appears in the same directory as the encrypted file.

## USING DIGITAL SIGNATURES IN PDFS

Traditionally, PDF files have their own form of security, which consists of two passwords: one to view the file and one to edit the file that includes permissions. These choices are available from *File | Export As | Export as Pdf…* | *Security*. However, they are easily cracked, so much so that only unsophisticated users are deterred by them. In fact, if security matters, you should not use them at all.

Instead, go to *File | Export As | Export as Pdf…* | *Digital Signatures* (Figure 4). As with other files, you can choose to use a certificate manager or GPG. You do not have to fill out the certificate password, since the information is contained in the certificate, but doing so is recommended. The other fields (*Location*, *Contact Information*, *Reason*, and *Time Stamp Authority*) are also optional.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_71_1.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_71_2.png)

A Time Stamp Authority, such as freeTSA.org [3] (Figure 5), is useful in cases where the information in the file is time-sensitive, or in cases where you need to approve an action before a certain date or time.

## RELATED SECURITY OPTIONS

A digital signature is not the only way to secure a LibreOffice file. For instance, from *Insert | Signature Line*, you can add a line for a hard-copy signature to be added to the document. While earlier versions of LibreOffice allowed a certificate to be used with this feature, LibreOffice 7.0 does not. Consequently, for a digital file, this feature does nothing for security or privacy.

More usefully, when you save for the first time or save a copy using *File | Save As*, you can also select boxes to *Save with password* and *Encrypt with GPG key*. Both choices will open additional options to set up these added security measures. In fact, you might prefer to use *Encrypt with GPG key* rather than using a digital signature at all, since encryption by itself should verify the validity of a file. However, for a higher level of security, you may want to use both these options, as well as a digital signature (Figure 6).

For many users, digital signatures and these additional features may require familiarizing yourself with a number of new concepts. But, contrary to your initial impressions, these concepts are not difficult, and some online research and experience should soon familiarize you with how they work.

Once you are comfortable with the basics, digital signatures and related features can give you strong security and increased privacy, both of which are badly needed given the insecurity of so much of modern computing.

## INFO

- [1] GPG: https://gnupg.org
- [2] Let’s Encrypt: https://letsencrypt.org
- [3] Time stamp: https://freetas.org/index_en.php

# EXPERT TOUCH

The *Linux Shell Handbook* is available now!
This edition is packed with utilities for configuring and troubleshooting systems.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_72_0.png)

The *Shell Handbook* provides a comprehensive look at the world inside the terminal window. You'll learn to navigate, manipulate text, work with regular expressions, and customize your Bash settings.

Here's a look at just some of what you'll see in the new Shell Handbook:

- Customizing Bash
- Pipes and Redirection
- Regular Expressions
- Text Manipulation Tools
- Systemd
- Bash Scripting
- Networking Tools
- And much more!

Make the *Shell Handbook* your permanent desktop reference on the world of the terminal window.

# GET PRODUCTIVE

## Inspecting the XML Code inside LibreOffice Files

### Digging Deep

You may have heard that LibreOffice files “are XML-based” or “use XML,” but when you try to open a Writer document in a text editor, you only see a binary blob. Learn how to access and modify the hidden XML content using scripts. **By Hans-Georg Eber**

**M**agine that you held a talk at your company’s recycling event last year, and you created a presentation and a hand-out to go with your talk – full of references to the old year 2018 and the new year 2019. Now you’re asked to do it again, so you launch LibreOffice, open the old documents – you want to reuse many of the slides – and start searching and replacing.

Want to skip the manual work? This article shows you how to do it. Granted, there is a learning curve. I will be talking about XML, Bash, and Python – three possibly new languages (one for data, two for code). At the end, you will be able to search, analyze, and modify LibreOffice files automatically.

For example, Figure 1 shows how all occurrences of “Linux” were replaced with “Windows” in an Impress presentation.

Opening a Writer, Calc, or Impress file in a text editor yields an uninspiring collection of seemingly random characters – there’s no intelligible content. But once you learn that these files are zip-compressed archives, things start to make sense. In order to peek inside such an archive, rename the file (or make a copy) so that the file name ends with .zip. Then you can use your favorite archive tool (or the command line tool unzip) to unpack the archive, and you will find a whole hierarchy of files (Figure 2).

![](img/e39350c3a7c0d527d71b0e4097a0ba66_73_0.png)

The most important file is **content.xml**, which sits in the top folder: It contains the text or data you entered in the LibreOffice application, and there are also links to multimedia elements (typically image files). You can open content.xml and the other XML files in a text editor.

Now, why would you want to inspect the XML code so thoroughly? There’s a multitude of practical applications that come to mind. For example, imagine you write a document that contains source code listing fragments in some programming language, and you would like to have key words highlighted.

Often, people will choose the quickest approach (that is, take a screenshot of a text editor window in which the code is displayed with highlighting enabled, and then paste that into the document), but that will prevent copying and pasting code from the document. It would be much nicer to simply enter the code verbatim and then have it formatted automatically. By looking at (and modifying) the XML data, you could do this, but that’s actually an advanced task, since it would require generating a new text character style from scratch and adding new nodes to the XML tree.

For this article, I will stick with two standard tasks: searching for key words in documents and automatically making small modifications to documents.

### A “HELLO WORLD” DOCUMENT

In order to get started, create a Writer document and put just one line of text into it: “Hello World.” Do not apply any styles or other formatting, and save the document to `hello-world.odt`. Now the exploration can begin: rename the fresh Writer file to hello-world.zip and open or decompress it with your favorite unzip tool – if you’re a fan of the command line and have a Unix-like shell (such as Bash), try:

```
mkdir hello-world
cd hello-world
unzip ../hello-world.zip
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_74_0.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_74_1.png)

If you prefer to click on stuff, read the “Unpacking Zip Files” box: Even though unpacking a zip file is simple enough, you might not want the contents to spill into your default documents folder, which could happen if you simply double-click on the file. Assuming that you have unpacked the archive to a new test folder, open that folder in a file manager or change (cd) into it in the Bash shell. You will find four XML files, two additional files, and three subdirectories. The XML files have the following purposes:

- **content.xml** holds the document’s text contents (Figure 4). I will describe this file in detail.

### UNPACKING ZIP FILES

Some years ago, unpacking a zip file required the installation of a third-party tool on Windows and macOS (then called Mac OS): WinZip and Stuffit Expander were some of the standard apps at that time, and only Linux came with unzipping preinstalled.

- When you double-click the zip file in Windows, Explorer will display the contents without permanently creating new files. Click on Extract All to create a new folder with the decompressed files. By default, Explorer creates a new folder named like the zip file (without the .zip ending).
- On macOS, double-clicking this .zip file might turn it into a .zip.cpgz file which is a gzip-compressed tar archive - not helpful [1]. If this happens to you on a Mac, use the command line to decompress. Alternatively, install a different archive program: Stuffit Expander [2] is still available.
- For Linux, choices depend on your choices for desktop environment and file manager. As an example, KDE’s Dolphin offers various options for treating zip files. Left-clicking the file will display its contents in the Ark program, while a right-click opens the context menu where Extract | Extract archive here, autodetect (folder) is the best choice (Figure 3).

Depending on your unzip tool’s default settings, the unpacked files might appear in the same folder that contains the zip file because LibreOffice zip files store those files in the top-level directory: In most cases, that is not what you want. If your unzip program provides an unpack to subdirectory option (like the one mentioned for the Dolphin context menu on Linux/KDE), use that.
