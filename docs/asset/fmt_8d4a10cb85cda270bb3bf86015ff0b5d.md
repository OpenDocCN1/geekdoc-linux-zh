
As soon as you get to the purple boot screen, press any key (my favorite is the spacebar), and choose your language from the list that appears by using the arrow keys and ENTER. Then, press F6 to open a little menu with a list of cryptic options (Figure 21-2). These are kernel options and can be used to turn off features that sometimes cause problems when you’re trying to start the computer. Use the arrow keys to go up and down the list and the ENTER key to select an option (an x will appear next to it). In the first instance, I recommend selecting `acpi=off`, `noapic`, `nodmraid`, and `nomodeset`. Then, press ESC to hide the menu, and try to boot from the CD normally by selecting one of the options in the main list and pressing ENTER. If that didn’t do anything, you might need to apply some good ol’ trial and error to the kernel options to find a combination that works for you.

### Try an alternate CD/memory stick

Some computers are simply unable to run the live CD. An alternative text-based installation CD is available from http://www.ubuntu.com/getubuntu/downloadmirrors#alternate/; you’ll have to download the CD image (.iso) file yourself and burn it to a disc before you can use it (see https://help.ubuntu.com/community/BurningIsoHowto/ for details). This installation method isn’t as user-friendly as the graphical installation from the live CD, but it’s much more likely to work if you’re having problems. You could also try installing from a USB memory stick, as described in Appendix A.

![](img/f7cef0df22f9dba5a41777808c98eece_415_0.png)

Figure 21-1: The purple boot screen is displayed when you first boot from the Ubuntu CD.

![](img/f7cef0df22f9dba5a41777808c98eece_415_1.png)

Figure 21-2: Disabling kernel options via the Ubuntu live CD boot menu

## I Get a GRUB Error

When you try to start your computer, you might be left with a black screen, which says that there was a GRUB error. This means there is a problem with the GRUB bootloader, which is responsible for telling your computer’s hardware how to start Ubuntu. Fixing these errors tends to involve typing a few cryptic-looking commands or booting off a live CD, so be prepared for that. You can find a short guide to handling common GRUB errors at https://help.ubuntu.com/community/Grub2#GRUB%20Errors/.

## I Get a Kernel Panic or the Computer Freezes

Kernel panics have a scary name for a reason. If you get an error message saying that there was a kernel panic, something pretty serious went wrong in Linux-land, and you’ll probably find that you can’t use the computer until you fix the problem. Fortunately, such errors are rare, and even if you do get one, you should be able to fix it without too much work. I should also note that kernel panics are only serious in that they make it difficult to run software on the computer—the physical hardware side of your computer won’t be damaged at all, so once you get the software working again, everything will be back to normal. So really, there’s no need to panic at all.

Freezes and kernel panics often go hand in hand, but they’re not necessarily the same thing. You’ve probably seen a computer freeze up before—moving the mouse or pressing keys on the keyboard does nothing, and the display stays frozen. If the computer freezes, all you can do is give it a minute or two to see whether it wakes up and, if not, restart the computer or turn it off by holding down the power button for a few seconds.

You can try a few things if you keep getting kernel panics or freezes, detailed in the following sections. If nothing seems to be working, ask for advice in the Ubuntu forums, and, with a bit of luck, you’ll soon be up and running again.

### Unplug Unnecessary Hardware
