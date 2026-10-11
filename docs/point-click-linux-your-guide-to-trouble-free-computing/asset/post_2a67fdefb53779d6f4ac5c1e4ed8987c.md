
## Point & Click Linux!

Other manufacturers have other little BIOS tricks. After you've become accustomed to changing BIOS settings you won't have trouble figuring them out. Only the first few times are hard. If you think carefully before you save, and make sure you read all the text on the BIOS setup screens before you start making changes (and take notes before you start hitting keys, so that you can return to the default settings easily), you'll figure it all out without fuss.

### A List of Common BIOS Access Commands

We compiled this list from various online sources. It is not complete, but covers some of the most common computer manufacturers' most popular products. If your computer isn't listed, try some of the most common access commands; you can't hurt anything by trying them. And if that fails, your computer or motherboard manufacturer's documentation or Web site is a sure source of information about your BIOS, and is the ultimate place to turn. You'll need to know your computer's exact model number (and possibly serial number) to get the right commands, because they vary from motherboard to motherboard, and computer manufacturers can (and often do) change motherboard suppliers in the middle of a production run without telling anyone.

- 1. Acer—F1, F2, CTRL+ALT+ESC
- 2. AST—CTRL+ALT+ESC, CTRL+ALT+DEL
- 3. Compaq—F1 or F10
- 4. Dell—400 F1 or F3
- 5. Dell—Dimension F2 or DEL
- 6. Dell—Inspiron F2
- 7. Dell—Latitude F2
- 8. Dell—Optiplex DEL or F2
- 9. Dell—Precision F2
- 10. eMachine—DEL
- 11. Gateway—F1 or F2
- 12. HP—F1, F2 or F10
- 13. IBM (PC) — F1
- 14. IBM E-pro Laptop — F2
- 15. IBM PS/2 — CTRL+ALT+INS after CTRL+ALT+DEL
- 16. Micron — F1, F2 or DEL
- 17. Sony® — VIAO F2 or F3
- 18. Tiger — DEL
- 19. Toshiba — ESC or F1

**If You Can’t Figure Out How to Change Your BIOS Settings…**

…make a boot floppy. Here’s how you do it in Windows:

1. Start Windows.
2. Place the *SimplyMEPIS* CD in your CD drive with Windows running.
3. Open a DOS Window (in Windows).
4. Go to the linux directory on the CD.
5. Insert a blank, formatted floppy disk in your floppy drive.
6. Execute *mkbootfloppy.bat*.
7. Reboot with the floppy in your floppy drive and the *SimplyMEPIS* CD in your CD drive. Your computer should now run *SimplyMEPIS*.

## Booting MEPIS

Linux is very methodical in the way it starts. Each function of your computer is tested. This means your Linux startup may be slower than in other operating systems, but sometimes “slow but sure” is best. Another thing that’s slowing things down is that you’re running your software from the CD drive instead of from the hard drive. CD drives are much slower than hard drives, to the point where anything you do from the LiveCD is going to seem like it’s happening in slow motion instead of at full speed. You’ll find that after you get MEPIS installed on your hard drive, everything will take place between two and ten times as fast as it does when you’re running from the CD.

## Why MEPIS Linux Asks for a Password

After the startup routine, the screen may either look funny, like static, or go blank for a second. Then you'll see a login screen that gives you two choices: "Demo" and "root."

![](img/01efe5dd076565746bf3678068ba155c_27_0.png)

It's best to start with the user name *demo* rather than use *root*, especially if you intend to connect to the Internet. This is a security measure, and is one of the big reasons Linux doesn't fall prey to the viruses and worms that plague the users of some other operating systems.

When you are logged in as a *user*—probably your own name once you get MEPIS Linux installed permanently—the only part of the system you will be able to change is your own data and things like screen color and some other appearance options. To install software or make any heavy changes to the system, Linux requires you to log in as *root*. If you are logged in as a *user*, malicious hackers can't easily install software you don't know about or perform other mischief.

Cats, children and well-meaning friends can't mess up your computer by typing in the wrong commands, either, as long as you are logged in as a *user* and not as *root*. In fact, when you do the actual Linux installation you'll be able to give other users their own user accounts so they can log in and use your computer without disturbing (or ever seeing) your private information, email or anything else you store in your computer. And each user can choose his or her screen colors and other custom features, too, including Web site bookmarks and favorite music. With Linux, a whole family can share a computer, but it can be a "personal computer" for each family member since each can have his or her own user login.

Only root gets to see everything. (That's going to be you, right?)

## Logging In

In "demo mode," the password for the demo user is **demo**, all lowercase. The root password is **root**, also lowercase. We'll show you how to change passwords (and add users) later, when we install MEPIS on your hard drive. But right now, let's go with these defaults. Enter them, click on the "login" button—or just hit your "Enter" key after you type in the password—and in a second or two you'll see your full, ready-to-use KDE desktop. If your PC has speakers, you should hear a few notes of music as the desktop appears.

![](img/01efe5dd076565746bf3678068ba155c_28_0.png)

If everything has gone right, you are now ready to work (or play) with Linux. If your computer is connected to the Internet through a network cable attached to a DSL line, cable modem or other high-speed "always on" setup, you should be connected to the Internet now. You can test this by clicking the "M" in the panel at the bottom of the screen, which starts the Mozilla Web browser that's included in **SimplyMEPIS**.

![](img/01efe5dd076565746bf3678068ba155c_28_1.png)

If your network is not operating correctly at this point—that is, if you're not able to view Web sites—you need to open the MEPIS system center and change your system settings. If you're online automatically, there is no need to do this, but it still might be nice to spend a minute looking at the System Center.

## Using the MEPIS System Center

![](img/01efe5dd076565746bf3678068ba155c_29_0.png)

To open the MEPIS System Center, click on the “S” icon on the main desktop.

The first thing you get when you open the MEPIS System Center is a login screen. This one asks for the root password, not your user password. While you’re running from the CD, the password is root. (You’ll change it to something more secure after you install MEPIS on your hard drive, of course.)

![](img/01efe5dd076565746bf3678068ba155c_29_1.png)

## The Magic Desktop-Clearing Icon

We just told you to click on an icon on the desktop. What if your screen is covered by an application window? Or two or three or 40 application windows? (Linux has no practical limit on the number of applications or windows you can keep open, so you really can have 40—or even 100—applications open at the same time.)

The answer is the View Desktop icon in the lower left hand corner of your screen, next to the small picture of the gear with a “K” on top of it. Click the View Desktop icon, and you’ll have a clear view of your blank desktop.

![](img/01efe5dd076565746bf3678068ba155c_29_2.png)

# 2: Running the SimplyMEPIS CD

Type in that password, and you’ll see the MEPIS System Center main screen.

On the left side of this screen, you see an index of functions, and above that index there’s a Help choice. If you click Help, you’ll see these words:

### Using the MEPIS System Center

To use the MEPIS System Center, just select a function in the Index tab and follow the instructions in this Help tab.

That’s how simple it is to use the MEPIS System Center. We’ll start by looking at Network Interface.

![](img/01efe5dd076565746bf3678068ba155c_30_0.png)

This screen tells us what our network is doing. In this example, we have an active wireless network connection. We see which network services are running because we have buttons available that allow us to stop them. If those services aren’t running, those buttons say “Start” instead of “Stop.” The buttons marked “Start eth0” and “Start ath0” are shadowed and barely visible because this computer was not attached to a wired (eth0) connection, just wireless, so no wired connection was detected.

Ath0 is used only for Atheros network cards, which aren’t terribly common. If you have one, MEPIS automatically detects it, automatically installs the right drivers, and automatically starts it for you.
