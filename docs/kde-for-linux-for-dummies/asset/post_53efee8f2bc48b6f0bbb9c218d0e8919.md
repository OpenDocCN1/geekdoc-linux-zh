
## IO Ports

- IO ports, or Input/Output Ports, can cause quite a bit of hassle if you don't know which device uses which port. An I/O device is anything attached to your computer that either provides data to the computer, or handles data created by the computer: keyboards, monitors, scanners, and so on.

## Partitions

- Don't know how your hard drive is partitioned? Check it here. (Partitions allow you to manage the space on your hard drive more efficiently.)

## PCI

- What's occupying your PCI slots? (Knowing this information can be very handy if you're faced with a great deal on an ebay auction, but you're not quite sure if you have any available PCI slots for the new toy.)

## Processor

- This tool gives you some extremely useful information about the processor on your motherboard. You can learn the type of processor, manufacturer, speed, and all the other information you need to get into a bragging war.

## SCSI

- Got SCSI devices installed on your machine? Check 'em here.

## Samba Stats

- If you're running Samba for your local network, you can check it out here. (Samba is a program that allows you to share files over a network with both Linux and Windows 95 or 98 computers.)

## Sound

- This tool is currently not supported. In future releases of KDE, it will contain information about your sound card.

## X Server

- For information about your X Window System server and useful if things go kablueey and you have to explain your set-up to someone who understands X. (And if you find that person, treat her nicely! Such people are worth a great deal.)

# Tweaking Your Keyboard and Mouse

True, most of us just plug in our input devices and go our merry ways. You can make your keyboard and mouse more responsive to your individual habits, though, with a few nifty KDE tools.

In the KDE Control Center, you find several keyboard tools that allow you to minimize the number of keystrokes it takes to perform a given action, to get your keyboard responding properly to the way you type, and to permit the use of non-English keyboards. Mouse tools let you set speed and responsiveness of the cursor. We also include a non-computer procedure in this section, so that you can keep your mouse clean and happy, thus avoiding one of the major reasons for mouse trouble.

## The mysterious configuration file

Keep in mind that KDE, despite its many graphical features, is still just an overlay on top of Linux itself. After you click an icon on the KDE desktop, the computer interprets that click as an issued command — the same as if you typed the command at a text prompt. KDE gives you the option to use graphical tools instead of learning the text commands.

```
# KDE Config File

[KDE]
widgetStyle=Motif
macStyle=off

[Global Keys]
Kill window
mode=CTRL+ALT+Escape

Pop-up system menu=ALT+F1
Window toggle sticky=
Window move=
Task manager=CTRL+Escape
```

In the same way, if you use the Control Center to change your mouse’s behavior or to set up a graphical login screen, you’re really editing your configuration files. A configuration file is a text file, and you have several scattered throughout your directories that control different facets. (You sound “in the know” if you refer to them as config files.)

The sample shows how we configure the basic appearance of KDE and a few global keystroke combinations.

To see a sample configuration file, fire up KFM and open your home directory. Choose View → Show Hidden Files. Now, in the file listing, look for a file called `.kderc`. This file is the main config file for personal KDE configuration for features such as icons, themes, global keys, and so on. Here’s an excerpt from the `.kderc` file on one of the computers we used to write this book:

You can find other personal configuration files in your `.kde` directory (be sure to include that leading dot). Config files for the whole system are located in various subdirectories under `/opt/kde`. (You may need to log in as root to view these.)

As a general rule, don’t muck around in these files for fun, or you may find yourself unable to use your computer. Knowing that the files are there, however, is still good. Should it come to pass that something is so broken that a KDE Control Center tool can’t fix it, or that your Control Center is somehow corrupted, you know where the config files are so that you can edit them by hand.

## Typing up a storm

If a hundred chimpanzees with Smith-Corona manual typewriters may eventually compose *Hamlet*, just imagine what you can do with a streamlined and personalized keyboard! You can configure several things in the KDE Control Center, including custom keystroke combinations, keyboard layout, and basic settings to match your typing style.

### The perfect (keystroke) combination

One of the more useful features you can do with your keyboard is to set up keystrokes, or combinations of keystrokes, that perform given functions. That is, you can assign a common action to a keystroke combination, rather than using a multi-click process to get the action completed.

You can see the standard keystroke combinations, already assigned by KDE, by choosing Control Center→Keys→Standard Keys. Don’t duplicate these when you create your own!

![](img/8dd43d91b80664e771e0c0a824d7392d_290_0.png)

To assign keystroke functions, choose Control Center→Keys→Global Keys. To give you an idea of how the process works, here’s how to set up your keyboard to manage your virtual desktops (see Chapters 1 and 3 for more information on virtual desktops). In this example, you set the keystroke combination Ctrl+→ (Control plus right arrow) to move to the virtual desktop immediately to the right of the one you’re now working on.

1. **Choose Control Center→Keys→Global Keys.**

   The Global Keys window appears, as seen in Figure 14-7.

2. **Select the Switch One Desktop to the Right option in the Action box.**

   The Action box is the area where you choose the action that you want to link to the keystroke sequence.

![](img/8dd43d91b80664e771e0c0a824d7392d_290_1.png)

**Figure 14-7:** Assign key- strokes to frequently used actions to automate the process.

3. Click the Custom Key radio button.
   With this button, you begin the process of defining which keys are to be associated with the action you choose.

4. Click the CTRL checkbox.
   Here, you set the keystroke sequence to include the Control (or Ctrl) key. Using the Ctrl key is a good idea because it requires you to perform the keystroke sequence intentionally. If you assign actions to single keystrokes, you run the risk of setting off actions while you're typing normally when you really want to use the keys for their original purpose.

5. Click the rectangular box that looks like a key.
   The key box is highlighted. The next key you press on the keyboard assigns the keystroke combination.

6. Press the right-arrow key on your keyboard.
   The word Right appears in the key box, and Ctrl+Right appears in the key table above the key box. Your window looks like the one in Figure 14-8 after you complete the task sequence.

7. Click OK.
   The Global Keys window closes, and your keystroke combination is complete. Now, each time you press the Control key and the right arrow key at the same time, your monitor shows the virtual desktop to the right.

![](img/8dd43d91b80664e771e0c0a824d7392d_291_0.png)

## Chapter 14: Taking Control — the KDE Control Center

Keystroke combinations are wonderful timesavers for frequently performed actions. You can easily go a little nuts with them and try to assign combinations to every action you may ever want to perform, but remembering just a couple of combinations is easier. Figure out what you do frequently that requires a lot of clicking or sequential menus, and assign those extra clicks to a keystroke combination.

![](img/8dd43d91b80664e771e0c0a824d7392d_292_0.png)

**REMEMBER**

You can always clear keystroke combinations by going back into Control Center \ Keys \ Global Keys and deleting that particular key association to the action. You may have chosen a key combo that isn’t quite intuitive enough if you can never remember whether it’s Ctrl-F3 or Ctrl-3.

![](img/8dd43d91b80664e771e0c0a824d7392d_292_1.png)

**TIP**

Give your brain a hand if you construct keystroke combinations. Use combinations that make sense, rather than combinations that are built almost wholly at random. To use a familiar example, doesn’t Ctrl-S for Save make more sense than Ctrl-9? Try to stick with combinations that use spatial or alphabetical triggers — psychologists say that such mnemonic devices make it easier for us to remember abstract information such as key combinations.

### Your keyboard’s a polyglot

Take a minute to think about this — not every language uses the same alphabet as English, right? How do you suppose people who write in other languages handle their keyboards? The trick is in keyboard layout configuration. You can find a keyboard suited to almost every language where computers are used; then, you just need to load the proper keyboard drivers into the system, and away you go.

If you want to use a keyboard different from the standard English keyboard used by Americans, Anglophone Canadians, and the rest of the English-speaking world, take a look at the list below. Given the international appeal of KDE, you’ll likely find a keyboard layout right for you.

- Bulgarian
- Canadian French
- Croatian
- Czech — KDE provides drivers for three different Czech keyboard layouts.
- English (Dvorak layout) — The Dvorak layout is different from the standard QWERTY keyboard. Afficionados of Dvorak claim this layout increases typing speed and reduces error.
- European (Western)
- Finnish
- French (Switzerland)
- French
- German (Switzerland)
