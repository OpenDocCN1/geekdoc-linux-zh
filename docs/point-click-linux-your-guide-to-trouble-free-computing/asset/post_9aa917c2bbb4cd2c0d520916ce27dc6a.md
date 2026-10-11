
You'll need to put the root password here. Remember, while we're still running from CD, it's root, but we're going to choose a more secure one during our installation.

![](img/01efe5dd076565746bf3678068ba155c_52_0.png)

## About hard drive partitions

Hard drives store data in the usual digital “on or off” style, but there are a number of different patterns in which they can be stored. Windows 95, 98, and ME use a method called FAT 32. Windows NT, 2000 and XP use a method called NTFS. DOS and really old versions of Windows use FAT 16. Linux uses a different method of data storage, and even uses different names for different drives. Windows usually calls floppy drives A and B, hard drive C, and CD drives D, unless there are two or more hard drives, in which case hard drives can be E and F and G and so on, with the CD drive becoming the letter after the last hard drive.

This illustration shows how Linux names drives:

/dev/floppy is a floppy, /dev/cd is a CD drive, and /dev/hda is this computer's single hard drive. There's also a tmpfs that's a temporary file system designed to speed up certain kinds of data access, originally developed for huge mainframe computers but also useful on your PC. There's also /dev/sda1, which is a flash memory card for a digital camera.

![](img/01efe5dd076565746bf3678068ba155c_52_1.png)

Now comes the cool partitioning stuff.

While Windows typically uses the whole hard drive as one big glob, you can make Windows run slightly faster by partitioning the hard drive so it acts like a number of small hard drives instead of one big one. This can also make system maintenance easier. If you keep all your pictures and text files in a separate partition from your programs, you can back up all your important data by simply backing up that partition.

MEPIS Linux uses three partitions—what you see in the previous illustration as hda2 and hda4, and another, very small hda3 “swap” partition (that acts like an expansion of your computer’s RAM) kept hidden. Note, too, that there is an hda1 partition. This is a Windows partition—the vfat next to the partition number tells us it uses the Windows FAT system.

The ext3 file system used by MEPIS Linux differs from FAT in many ways, but the most obvious one is that if power to your computer is removed or you turn it off without going through the “correct” shutdown procedure, you can start it right up again without any problems. This is a feature even the latest versions of Windows don’t have.

One last trick with the MEPIS Linux file system: It stores all your personal data in a /home partition by default—and not just your photos, text and music, but things like your favorite Web site bookmarks, your email, and even your desktop settings and other customizations, so you can easily upgrade or even reinstall MEPIS Linux without having to do a lot of setup or data restoration afterwards.

Now we get to the hairy part: actually partitioning our hard drive.

Right now we’re at the Install screen, getting asked how we want to do our install.

![](img/01efe5dd076565746bf3678068ba155c_53_0.png)

## 4: Installing MEPIS Linux on Your Hard Drive

We choose Custom Partitioning. This brings up the QParted utility.

We click on hda to work with our one hard drive. (QParted allows for multiple hard drives. This is why we must click on the one we're interested in changing—even if the PC we're using as an example here only has one.)

![](img/01efe5dd076565746bf3678068ba155c_54_0.png)

We can now see the one big Windows (FAT) partition. To shrink it, we “grab” the right end and move it to the left, which makes it smaller. The screen gives us a minimum amount of space we must allow. It's good to allow at least 20% more than this, and 50% more is better, just in case we need to add some more Windows files someday.

To actually make the change—at this point we can still change our minds—click on the little image of a floppy disk, which is the near-universal symbol for “save,” except in QParted it's called “commit,” which is more accurate here because when we commit to changing a partition we can't undo our decision. So let's do it and get it over with.

Now we have a large unassigned space to the right of the Windows partition. This is where we're going to install Linux.

We want to make three Linux partitions. The first one, called mount, is where all our programs will go. Select ext3 as the partition type. We want this partition to be at least 3GB, possibly as big as 5GB. Then we commit. Next, we add a

![](img/01efe5dd076565746bf3678068ba155c_54_1.png)

small partition type called swap, which acts as additional RAM memory in case we use up all our “real” RAM. This partition should be about as large as the amount of RAM memory we have, although this is not critical. Make it 512MB (MB, not GB), and you’ll be fine. Our third partition is also ext3, and it’s our *home* partition.

Our hard drive is now split down the middle, half for Windows and half for Linux. We’re done partitioning.

### Installing Linux by Itself

Let’s go back a few steps to where we were asked what kind of install we wanted. If we want to install Linux all by itself on our hard drive, all we need to do is select “*Auto-install using entire disc*” and go from there. Much easier!

![](img/01efe5dd076565746bf3678068ba155c_55_0.png)

After we make this selection and click “Next,” all we need to do is sit back and watch as MEPIS automatically formats our hard disc and installs itself.

![](img/01efe5dd076565746bf3678068ba155c_55_1.png)

The little bar will crawl across the screen as MEPIS installs. This is going to take between five and 30 minutes, depending on your PC’s speed. Now is a great time to get up, stretch, grab a cup of coffee or a glass of soda, juice or water.

## Names and Passwords

The next human intervention required for your MEPIS installation is saying “Yes” when you’re asked if it’s okay to install the GRUB (GRAnd Unified Bootloader) utility in the MBR (Master Boot Record). Go ahead; if you’re an advanced Linux user you can customize your MBR later. The rest of us will be satisfied with plain-jane GRUB. It allows us to boot Linux in more ways than most of us ever need and gives us the ability to boot multiple operating systems, like Windows and Linux next to each other—or even two or three different Linux installations, if we like.

Our next task is deciding on a user name, a root password, and—if your computer is part of local network—typing in the network’s name and giving your computer a name that will identify it to other computers on the network.

![](img/01efe5dd076565746bf3678068ba155c_56_0.png)

The user name can be anything you like. You can add more users later. Both the user and root passwords ideally should be a mix of numbers and letters at least six characters long, rather a relatives name or something else that can be figured out by a lucky guess.

## The root password is important!

The root password is one of the most critical pieces of information you need to put in while installing your new MEPIS Linux system. If you know your system's root password you can change user names and passwords later, but if you don't remember your root password you can't change anything important without going to the trouble of installing everything all over again.

The root password is your main line of defense against malicious hackers. You want to make it very hard, ideally impossible, to guess, hopefully by using a long string of randomly mixed letters and numbers along the lines of 32x49xrtgw05567. The problem with this kind of hard-to-crack password is that unless you have an excellent memory, you are going to forget it, so you'll need to write it down somewhere. Then you need to make sure the paper you wrote it on is hidden from prying eyes.

So maybe you choose a less exotic password. At least make sure it's not a real word. And throwing a number or two in the middle can't hurt. That ought to be secure enough for non-government work. Just make sure you don't use this password on a Web site or someplace else it might be revealed to the rest of the world by mistake.

You only need to use your root password when you install or delete software, add or delete users, or otherwise alter your computer in some way. You won't use it every day. If you go the "write it down" route, it's better than forgetting it—assuming that you don't forget where you hid the paper you wrote it on, as this book's author did with a root password several years ago...

There are only a few more MEPIS installation screens. The first one is for Samba networking with Windows computers on a network. This can be set up later, and more details will be covered in this book's "Beyond the Basics" section. For now, just click "Next." The final screen is for security and dialup. Those who use dialup Internet connections will find full instructions on how to set them up in Chapter 5, "KPPP—Easy Modem Dialer Application." And on the security front, MEPIS automatically sets up a Guarddog firewall utility, and you should have a firewall on any computer you attach to the Internet, no matter what operating system it runs, so just click "Next" here instead of changing anything.

![](img/01efe5dd076565746bf3678068ba155c_57_0.png)
