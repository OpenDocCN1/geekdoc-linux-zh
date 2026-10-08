need a Windows 2000 operating system license. Wine provides all the library hooks and sundry items to run an application like Word 2000.

![](bbox=[0.11, 0.17, 0.19, 0.27])

Wine is continually modified and updated to remain as compatible as possible with Microsoft. Wine occasionally has trouble, however, running such complex applications as Office and Word. If you encounter this type of problem, please consult our help page at www.dummies.com/go/rhlfedoraf4 for possible fixes. You can also use commercial Wine variants, such as CrossOver Office, to run Office or Word.

![](bbox=[0.23, 0.31, 0.7, 0.62])

![](bbox=[0.14, 0.48, 0.22, 0.6])

Go find your Word 2000 (or Word 97, Word XP, or whatever) disc and get ready to rumble. These steps show how to install and use that word processor:

+   1. **Log in to your computer as a nonroot user and insert the Microsoft Word 2000 CD into the CD-ROM drive.**

   These steps should work reasonably well with a Microsoft Office 2000 CD.

2. **Click the GNOME Menu and choose System Tools->Terminal.**

   The Run Program window opens.

3. **Enter this command in the text window:**

```
wine --dll cabinet=n /mnt/cdrom/setup.exe
```

You may have to substitute cdrom1 for cdrom if you have two drives.