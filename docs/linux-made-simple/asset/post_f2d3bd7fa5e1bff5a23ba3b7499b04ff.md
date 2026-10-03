
Now navigate to the folder where the **SteamOSInstaller.zip** was downloaded (usually Downloads), for example:
then type in
where **/path/** is the path of your USB drive. Next, you'll need to install the USB stick into the machine that you're using for the installation. With the USB stick installed, start up the PC and load up the BIOS. This can usually be done by repeatedly tapping F8, F11, or F12 as soon as your system is turned on.

```
cd ~/Downloads/
```

```
unzip SteamOSInstaller.zip -d /path/
```

Once in your BIOS make sure that UEFI support is enabled and select the UEFI entry to boot from.
If you don't mind having the entire hard drive formatted and replaced with SteamOS, select the Automated install option from the menu when it appears. If you have additional disks and partitions that you want to keep, and you want to install SteamOS in a select location choose Expert install.
If you've ever used the Debian installer you'll be pretty familiar with what comes next. First, you'll be asked to choose your language,

location and keyboard layout. The installer will then begin setting up your hardware which will usually take a few minutes. Once done you'll see your hard drives and partitions. This is where you can decide which partitions and drives to use to install SteamOS – useful if you don't want to use all of your hard drive or if you're planning on going the dual-booting route with SteamOS for gaming and another distro for day-to-day tasks.
Select the free space for installing SteamOS – it should be a minimum of 10GB. Select Create a New Partition if you need to and specify the size. Ensure it's Primary, then click Continue, making sure in the Use as Area it has Ext4 Journaling Filesystem, then select Done setting up the partition.

Click on the free space to create another partition. Give it a size of around 10GB – this will be your swap partition. Make it logical, and create it at the end of the available space when the options appear. When you get to the summary screen, double-click Use as and select Swap Area. Double-click the remaining space, leave the partition size as it is and make sure where it says Mount Point you have it set to /home. Select Finish Partitioning and Write Changes to Disk, then select Yes. SteamOS will begin configuring and installing itself.

Once done a window will appear called Software Selection asking you if you want to install the Debian desktop environment and standard system utilities. Keep both of these ticked and click Continue. Once done your PC will reboot.

Once your system has rebooted, you'll be given the choice to start SteamOS or start it in Recovery Mode – leave it to start normally and SteamOS will continue the installation. Make sure your machine is connected to the internet, as Steam will be installed. Once that's done your machine will reboot once again. The process might create the rescue partition now, so let it do its thing and select to reboot. You'll then be presented with a Debian login screen. Select SteamOS Desktop and click Return to Steam.

If this doesn't work, open up the Terminal and type steam. Accept the terms and click OK. There may be some more downloading to be done, but once that's done you'll be thrown into Steam's Big Picture Mode where you'll be able to log in to your existing Steam account, or create a new one.

Alternatively, If you don't want to install a new OS for Steam you could install the Steam for Linux client instead on any Debian-based distro by typing in apt-get install steam or aptitude install steam. You're now ready to enjoy over 1,000 (and counting) titles.

## Peripherals

So you've built an amazing, yet compact, Steam Machine and loaded up SteamOS. Now what? You'll want to get some great gaming peripherals for comfy gaming from your sofa. Valve itself has been working on a dedicated Steam controller with the lofty ambition that it will combine the convenience of a game controller with the precision of a keyboard and mouse setup. It's certainly a tall order and one that Valve appears to have struggled with as the controller has been delayed until late 2015. While we wait for Valve's official controller, which will cost $50, a number of other companies offer some great alternatives for controlling SteamOS games. Roccat has built a Sova lapboard especially for SteamOS which offers a small mechanical keyboard and large mouse pad that can rest on your lap. You can also use games controllers from game consoles, such as the Xbox 360 and PS4 as SteamOS does a good job of recognising them as soon as you plug them in. If you're a fan of racing games then the good news is that renowned racers, such as *Project Cars* are coming to Linux. What's not so great is the support for steering wheel controllers.

If you have a Logitech controller you can install the LTWheelConf tool. Full instructions on how to use it can be found on the Steam network (http://bit.ly/LTWheelConf).

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_0.png)

The Roccat Sova has been built especially for SteamOS devices.

## The 20 best games on Linux

### Five best open source games

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_1.png)

**Strife: Veteran Edition**
This is an awesome first person shooter built on the open-source Chocolate Doom engine. Grab the game from http://bit.ly/StrifeVE.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_2.png)

**Stunt Rally - version 2.5**
Race and performing stunts in fantastic environments. This game features 167 tracks, 19 cars and a track editor. Download the game at http://bit.ly/StuntRally.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_3.png)

**Annex: Conquer the World 4.0**
If you enjoy real time strategy games, then this open source game is for you. Download the game from http://annexconquer.com.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_4.png)

**BYOND: Space Station 13 Remake**
This remake of a criminally overlooked classic is completely open source. Download the code from http://bit.ly/SS13Remake.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_5.png)

**Galaxy Forces: Moon Lander Action!**
Hark back to a simpler time for games with this retro-fuelled moon lander shoot-em-up. Download from http://bit.ly/GalForcesV2.

### Five best AAA games

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_6.png)

**The Witcher 2: Assassins of Kings**
An epic tale of monster-slaying and alchemy. *The Witcher 3* is coming soon, but play this first.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_7.png)

**Dying Light**
An action survival game presented in first-person. Navigate a dangerous zombie-filled open world to help survivors.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_8.png)

**Borderlands 2**
This fun and frantic first person shooter makes a post apocalypse world seem like a lot of fun. Play in co-op mode with friends.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_9.png)

**Amnesia: The Dark Descent**
Games don't come much scarier than this, so if you're after a good horror game then you'll love this.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_61_10.png)

**Broken Age**
The first graphic adventure by Tim Schafer in sixteen years, funded by a record-breaking Kickstarter – and well worth the wait.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_0.png)

Big Picture Mode makes launching games on a TV with a games controller quick and easy.

## Ten best indie games

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_1.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_2.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_3.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_4.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_5.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_6.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_7.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_8.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_9.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_62_10.png)

**Hotline Miami 2: Wrong Number**
The sequel to the ultra-violent and maddeningly addictive indie sensation comes with the same thrills and amazing soundtrack, but it's not for the faint hearted or kids.

**Supreme League of Patriots**
A classic point and click adventure game with very modern sense of humour brings a cast of crazy characters and fiendish puzzles and combines it with a great art style.

**The Fall**
The first story in a trilogy, this adventure game excels at world building, story and atmosphere. You play ARID, an artificial intelligence onboard a high-tech combat suit occupied by an unconscious pilot.

**Dungeons 2**
If you're a fan of Bullfrog's classic game Dungeon Keeper then you'll love this spiritual successor, which not only allows you to build devious dungeons to thwart pesky heroes but sees you go topside to attack cities.

**The Binding of Isaac: Rebirth**
This is a randomly generated action RPG shooter with Rogue-like elements. If you don't understand what we just said, all you need to know is that it's a lot of fun.

**This War of Mine**
A game like no other. You don't play as an all-powerful soldier, but instead a group of civilians just trying to survive in a besieged city.

**Chivalry: Medieval Warfare**
Besiege castles and raid villages in this fast-paced medieval first person slasher with a focus on PvP.

**Papers, Please**
Play the role of immigration inspector for a fictional country. Bureaucracy might not seem thrilling, but this manages to make it so.

**FTL: Faster Than Light**
Take your ship and crew on an adventure through a randomly generated galaxy filled with glory and bitter defeat in this spaceship sim.

**Goat Simulator**
Ever wanted to play as a goat? This offers you a chance to live the dream in this completely realistic (not really) simulation.
