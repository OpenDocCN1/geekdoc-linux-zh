
## Figure 4-1

The GNOME Control Center.

If you find another picture sometime that you like on the Internet, you'll be able to change your background. And other backgrounds will be made available with new releases of Red Hat Linux, so keep an eye on the upgrades.

## Screensavers

You have a lot of choices when it comes to screen savers. GNOME allows you to preview the selected screensaver (though some will have problems), so scroll through until you find one you like. You use the bottom buttons for screensavers the same way you used them for backgrounds. (Clicking “Try” really won’t do anything, however.)

My personal favorite is Boboule.

Like the background images, more screensavers are being packaged with Red Hat Linux every time it’s released. You’ll want to keep an eye on upgrades and various packages that you can download using the GnoRPM utility. (See Chapter Six for a discussion of GnoRPM and downloading upgrade files.)

### Theme Selector

The theme selector allows you to get rid of the rather drab default color scheme that comes with GNOME. Make good use of the preview box. You’ll appreciate being able to see what each looks like before trying it out.

You can also use your own font scheme if you’d like. Most themes come with a default font in use, but these are occasionally not up to par. Some may be too small or simply don’t match very well. Uncheck the “use default font” box if you’d like to specify one. (The box below will become active, that is, it will no longer be “grayed out.” Click on this box to choose from a list of available fonts and sizes.)

If you’re particularly adventurous, you can also use what are called “pixmaps” to further customize the look and feel of your windows. A sample theme called “pixmap” comes with GNOME to show you how it looks. (It’s one of my favorite themes, incidentally.)

Make sure to apply and accept the changes you’ve made. You can always try them out before you do to make sure you like them.

The theme selector here will control how your desktop and certain aspects of your windows look—but it won’t change some of the features that we’re going to change when we configure Enlightenment.

### Window Managers

In this section you can add, remove, or configure various window managers. Though you’ll probably only see Enlightenment in the list, you do have some others. Since Enlightenment is the default window manager and probably the best available, we won’t worry about the others for now. (If you consult the references list at the back of this book, you will find search engines that will find various window managers for you. When we talk about system upkeep we also touch on this subject again.)

What you’ll probably want to do is click on the button marked “Run Configuration Tool for Enlightenment.” The new pop-up window allows you to customize how Enlightenment works. The screen itself looks like this:

![](img/92fb6d8ad19de3b3470ba95c7b71b82e_77_0.png)

## Figure 4-2

Enlightenment’s Configuration Editor.

### Configuring Enlightenment

There are a number of categories to choose from that you can use to make modifications. Most of these are self-explanatory, but a few do require some comment.

#### Desktops

Your desktop is your working environment—it’s where windows open, where icons are placed, and where you interact with the computer. This section is where you can modify how your desktops “work”—what properties they have.

Unlike Windows or the Macintosh OS, the X-Window System makes use of multiple desktops. If you examine the panel at the bottom of the screen, you will notice that there is a space where there are four squares. If you click on each of them, a fresh and likely empty desktop will appear. (It will have its own panel and desktop icons, however.) This is what is meant by multiple desktops.

This is *not* the same as having more than one monitor attached to your computer. Some operating systems (Windows included) will allow for “multiple desktops” by using another monitor. In Linux, you can have many, many desktops (as many as 2048!) using only one monitor.

In the desktops category, you can select the dimensions of your extra desktops—that is, will you have a two-by-two grid or more or less? You can also select how many layers of these desktop grids you want—up to 32 of them.

If you want to change between desktops without clicking on the squares below, you can enable what is called “Edge Flip Resistance.” When you bring your mouse down to the edges of a desktop, it will “flip over” to the next. You can adjust the sensitivity with the little bar below.

#### Behavior

One of the more annoying idiosyncrasies of the X-Window System—at least for those who are more familiar with Windows 95 or Windows 98—is the concept of *window focus*.

When you start running a program in X-Windows, the focus isn’t automatically adjusted to the program. If you click on the main menu button and then “run program,” you’ll notice that you can’t type in a program name unless you click on the window first. This is because the focus has not been shifted to the window yet. You’ll have to click on it before you can type anything in the window.

In the “Behavior” window, you will be able to modify how the focus shifts every time you “mouse over” (move your mouse over) a window or start a program. Set it to your liking.

#### Audio

If you want to use sound effects while running Enlightenment, click yes; otherwise, click no.

These sounds are relatively elementary, consisting mostly of beeps; users more accustomed to the waveform sounds (waveforms are the same as .wav files) of Windows may be somewhat disappointed in the array of sounds available.

#### Special Effects

Leaving this customization at defaults is just fine. If you want to enable any of the special effects listed here, just click on them.

#### Backgrounds

Not only will GNOME provide you with the chance to change your background, so will Enlightenment. Enlightenment comes with some prepackaged background pictures (quite pretty pictures, if I might add my opinion) and some rather simple graphics to choose from. You can also use a blank background if you'd like.

You'll notice if you use these backgrounds that the one you selected in the control center will conflict with the one you select here. If you'd rather use the one you selected in Enlightenment, tell GNOME not to use a background at all.

#### Themes

Enlightenment also provides stylized themes with special cursors and window modifications that you can experiment with. Themes can greatly enhance the look of your windows. Several come with Enlightenment, but you can get many, many more.

The prime place for themes is www.themes.org. Themes.org is a wonderful place to get absolutely free and stunningly gorgeous themes. The site is packed with other graphics information, too, so if you're looking for development information, you'll be able to find it here, too.

If you're interested in installing new themes, look at Chapter Six, which talks about maintaining your system. Read the section entitled, “Adding Eye Candy.”

#### Shortcuts

Enlightenment also offers several command-key shortcuts that you can modify, add to, or remove. If you find using mice rather pesky and annoying, you might *bind* a few commands to shortcut keys. (For instance, a default shortcut is to use Alt-F1 to move to the first desktop. Alt-F2 will move to the second, and so on.)

## Finishing the Configuration

After you've finished modifying Enlightenment's configuration to your liking, accept the changes and close it out. This covers much of your personalization of the GNOME desktop system, but we've still a few more subjects to consider.

## Adding Desktop Applications

If you made certain disks user-mountable, you noticed that new icons appeared on your desktop. If you want to add your own, you should right-click on the desktop. Mouse over to “new” and click on “launcher.” A *launcher* is the Windows equivalent of a shortcut.

After clicking on ‘launcher,’ a new window will pop up. You should see two tabs, one labeled “basic” and the other “advanced.” You won't need to make any changes to the advanced tab. In the basic tab, you should fill in the categories appropriately.

- **Name**: Type in the name that you want to show up on your desktop. This doesn't need to be the actual command name.
- **Comment**: Type any comments here that you have about the launcher.
- **Command**: This is where you'll write the command line for the program. If the program is in a directory in your path, just type in the command; otherwise, you'll need to specify a path. (Since we haven't covered the Linux file system, we haven't really discussed paths yet. Don't worry if this sounds confusing.)
- **Type**: You are creating either a directory or an application launcher. If you want to run a program, switch this from directory to application.
- **Icon**: The X-Window System comes with a variety of icons pre-installed. You can choose from them or from one that came with the program.
- **Run in Terminal**: If this program is a text-based program, you should *enable run in terminal.* Otherwise, leave this unchecked. (Unchecked options are usually gray.)

## Customizing Your Panel

Some users prefer to leave their desktops relatively uncluttered and would rather include these programs either as *applets* (small applications) on their panel or as launchers on their main menu. This process is fairly simple and
