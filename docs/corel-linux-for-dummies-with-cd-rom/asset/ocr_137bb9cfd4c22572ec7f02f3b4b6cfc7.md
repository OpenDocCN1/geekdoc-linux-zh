# # Changing Your Boot Defaults

![](bbox=[0.08, 0.18, 0.22, 0.3])

Let's say you converted your Windows machine to a dual-boot Linux/Windows system. You normally boot up and do all your work, Web browsing, and e-mail in Linux, and only occasionally use Windows programs when there's no close substitute.

But your spouse, well, just hasn't gotten around to changing from the old ways and goes berserk when the machine boots up to Linux. "I don't want this . . . how do I get out of this screen?" (How come kids never say that?) The best way out of trouble, in this case, is to change your Corel Linux Loader (LILLO) to boot to Windows by default.

![](bbox=[0.08, 0.43, 0.22, 0.54])

This is an advanced operation that involves messing with your *master boot record*. If you screw up, your machine might not boot until you restore the boot record. I'm assuming that you're a responsible child or maybe an adult. Otherwise, how did you get root access?

If you have an inkling of what you're doing, here's the trick:

![](bbox=[0.15, 0.6, 0.25, 0.69])

+   1. Log in as root, click the Text Editor button on the panel, and open the `/etc/lilo.conf` file.
+   2. Among the list of boot selections, find the label for the multiline section describing your Windows boot partition, as shown in Figure 4-24.
+   
+   The label is probably near the bottom of the OS pecking order. You'll see the likes of label=dos or, in this example, label=MS_Windows.
+   
+   3. On a line near the top of the file, above the list of boot selections, add `default=dos` (or whatever the selection is labeled).
+   
+   In Figure 4-25, I added the line Default = MS_Windows, to match the label of the Windows partition shown in Figure 4-24. I also changed the boot-up delay from 300 to 100 (10 seconds). For more on using the Text Editor, see Chapter 13.
+   
+   A trickier way to make Windows the default is to move the section describing the Windows section to the top of the pecking order.

![](bbox=[0.1, 0.74, 0.22, 0.86])

+   4. Do you want to adjust the time your computer waits before going on if you don't press a key? Change `delay=300` (30 seconds) to another value, as I did in Figure 4-25.
+   5. Click the Save button on the toolbar to save your changes.

![](bbox=[0.15, 0.9, 0.25, 0.95])