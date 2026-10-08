Depending on the state of Wine you installed, you may see a Microsoft Word 2000 Setup window informing you that it can’t find a font. Missing fonts generally don’t affect the functionality of the application.

4. **Click the OK button whenever a missing font warning appears.**

The installation process displays lots of information as it proceeds. You can ignore the lines as they pass by. They don’t affect the installation process.

The Microsoft Word 2000: Welcome window opens.

5. **Enter in the five text boxes the product key from your Microsoft Word 2000 disc (or from the physical package in which Microsoft enclosed the disc).**

Remember that Wine provides only the *platform* on which to run valid Windows applications. It doesn’t provide the applications.

6. **The next window you sees you the option of installing a standard Word configuration or, optionally, customizing the installation.**

For simplicity, we suggest that you click the Install Now button. (We leave it to you to navigate through the various additional configuration steps if you choose the Customize option.)

The installation continues until you’re prompted to reboot your computer. You’re not running a Windows computer, of course, so click the No button. The installation process seems to end.

7. **Wine provides a Windows reboot simulation utility. Repeat Steps 2 and 3 and enter this command:**

```
wineboot
```

The installation process starts up again and finishes. You have installed Microsoft Word 2000 on your Linux computer!

8. **You can start the word processor by repeating Steps 3–5 and entering this command in the text window:**

```
wine "C:\Program\Files\Microsoft\n
Office/Office/winword.exe"
```

![](bbox=[0.13, 0.74, 0.2, 0.81])

Backslashes (\) are escape characters in the Linux world; in the Windows world, backslashes separate directory names. That is, they prevent Linux (the bash shell) from interpreting the following character literally. Without the back-slash, Linux (bash) interprets the directory name `Program Files` as two separate entities, Program and Files, because the bash shell figures that the space character is a separator and not part of a directory name or filename. Therefore, the combination of a backslash and a space—`Program\Files`— allows Linux to process the directory name correctly: Program Files. The preceding command (refer to Step 8) is interpreted by Linux as `wine C:\Program\Files\Microsoft\n Office/Office/winword.exe`.