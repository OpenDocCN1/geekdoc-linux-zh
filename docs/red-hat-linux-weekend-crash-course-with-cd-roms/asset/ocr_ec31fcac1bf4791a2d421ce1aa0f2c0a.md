by a linefeed. The printer reacts to carriage returns and linefeeds the same way as old-fashioned typewriters — linefeed advances to next line and carriage return moves to beginning of a line. When printing a DOS text file, the lines print one after another as expected. However, when the printer prints a Linux text file with lines ending in a linefeed only, the output looks something like this:

```
Line 1 ends here
        Line 2 here
                and so on
                        like a staircase.
```

To avoid this staircase effect, just check the box marked Fix stair-stepping of text in the dialog box of Figure 4-6 and Red Hat Linux takes care of the problem by sending a carriage return before each linefeed whenever you print a text file. After you select the options in Figure 4-6, click OK in successive dialog boxes until you return to the main print tool window shown in Figure 4-3. This window should now show the information about the new printer. From the main window shown in Figure 4-3, you can then print a test page by selecting Tests ⇒ Print ASCII test page from the menu.

![](bbox=[0.04, 0.41, 0.14, 0.51])

# REVIEW

This session showed you how to overcome some common installation problems by running the installation in different modes. You learned how to use the text mode installation and how to use expert mode to install devices that the installation program does not detect. Finally, you learned how to configure X and printers.

# QUIZ YOURSELF

+   1. How do you start the installation in text mode? (See “Installing in Text Mode”.)
+   2. What do you do if the Red Hat installation program does not detect your network card? (See “Installing in Expert Mode”.)
+   3. When would you manually configure the X Window System? (See “Configuring the X Window System”.)