
2. If you don't find the icon for the program you're looking for, try installing the Main Menu application from the Software Center. Once it's installed, start Main Menu and find the application you're looking for by navigating through the menus. Right-click the name of your program and choose Properties from the menu that pops up. When the Launcher Properties window appears, take a look at the contents of the Command—for Tomboy it should be tomboy --search (Figure 21-5). You can ignore everything after the first space (only the first part matters), so in this case, the program’s command name is tomboy.

![](img/d35fa962e6f9664d66dc83916f426418_393_0.png)

Figure 21-5: Finding the command name for Tomboy using Main Menu

3. With the command name, press ALT-F2 to open the Run command of the Dash again.

4. Type ubuntu-bug tomboy (replacing tomboy with the command name for your program) and press ENTER.

The bug-reporting tool will start and collect some information about the program (such as what version you're using). Next, it'll ask whether you want to send this report to the developers—you do, so click Send Report, and a web page will open (log in to Launchpad if you haven't done so already). Type a brief description of your problem, being as specific as possible, and click Next.

## Has It Already Been Reported?

Lots of people are using the same programs as you, so there's a good chance that someone has gone to the trouble of reporting your bug already. Launchpad will go off to look for existing bugs that it thinks the description you gave, take a look at the list that appears and see whether any of the results sound familiar (Figure 2-6). If you find one, click the arrow next to it, read the description to make sure, and click Yes, this is the bug I'm trying to report. This could be a good sign, because someone might just be working on a fix!

![](img/d35fa962e6f9664d66dc83916f426418_394_0.png)

## Report a bug

Please describe the bug in a few words, for example, "weather app crashes on login":

Summary: Chromium crashes after opening a new tab [Check again]

Do any of the following bugs describe the bug you're trying to report?

- #8679 Crash when signing login screen in gdmsetup (Fixed in (5 comments) last updated 2024-04-01 view this bug)
- #5820 pdf signup (Fixed in (3 comments) last updated 2024-11-01 view this bug)
- #2760 Crashes when Cancel is selected in the GFileSelectionDialog (Fixed in (5 comments) last updated 2024-11-06 view this bug)
- #12978 Crash in viewModel (Fixed in (2 comments) last updated 2025-02-16 view this bug)
- #11903 Crashes When Making a Signature (Fixed in (3 comments) last updated 2020-07-15 view this bug)
- #17233 Many keys suddenly bound to incorrect actions

Figure 2-6: A list of bugs that Launchpad thinks are similar to the one you're reporting

Choose Just the bug as affecting me and click the green button to go to the bug page (the alternative option, Subscribe me as, which means you will receive an email every time someone posts a comment about the bug). Take a look at the comments that others have made about the bug and see whether anything could help you work around the problem. Comments are sometimes technical in nature, so it might be necessary to ask around on the forums for help with some of the more cryptic instructions. If you can't find anything helpful, you can try to provide more details on the problem to help a developer track it down. The developer will often ask you to provide a copy of the output of some command, which can help determine what is going wrong. If you think you can help, scroll down to the bottom of the bug page and put what you know in the comment box.

## A New Bug

If one else seems to have the same problem, then you've got a live one! Click No, I need to report a new bug at the bottom of the page where the list of suggested bugs appeared and write a description of the bug in the Further information box. Here are some tips on how to write a breathtakingly beautiful report:

- Report only one problem per bug. If you report more than one problem at a time, it will be difficult for the developers to keep track of what they've fixed and what they haven't.

- Describe what you were doing at the time the bug occurred. Context is important, so you should describe what you were doing when you experienced the problem. For example, if your music player crashed when you plugged in your iPod, you should mention that.

- Mention which version of the program you are using. The bug-reporting tool should have automatically provided information about software versions, but it's a good idea to make a note of yourself. Selecting Help > About in the program's menu will usually give you the version of the program, and you can find out which Ubuntu version you're running by clicking the power button on the top panel and select System Settings from the pop-up menu. Double-click Details in the window that appears.

## What Happens Now?

Once you've submitted the report, you'll receive an email confirming that your bug was received, but this isn't the end of the story. If you've reported a bug, keep an eye on your email. You will be notified every time the bug is changed or a comment is made. If someone asks for more information on the problem (Sebastien did with mine), all you need to do is reply. Your reply will be added to the bug report for everyone to see. The more information the developers have, the faster they will be able to fix the problem.
