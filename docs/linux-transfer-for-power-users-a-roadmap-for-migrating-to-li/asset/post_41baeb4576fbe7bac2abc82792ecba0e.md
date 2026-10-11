
![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_150_0.png)

> *Figure 35. The System Monitor applet has several views of the running processes on your computer.*

The **Resource Monitor** tab provides graphical displays of CPU load, as well as Memory and Swap history, mapped against time, as shown in **Figure 36**. The usage of storage devices is shown in the **Devices** list box; it’s the quickest way to see disk space usage at a glance—both for local and networked drives.

I found this applet to be very useful to learn more about my machine when I was getting started, and I still use it to keep tabs on unusual circumstances—sort of a “management by exception” approach.

## Clock

The panel comes installed with the Clock applet, which displays the time. You can configure this applet by right-clicking it and selecting **Preferences** to bring forward the **Clock Preferences** dialog as shown in **Figure 37**.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_151_0.png)

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_151_1.png)

You have four choices for clock type: 12 hour, 24 hour (my favorite), Unix time, and Internet time. The first two are obvious but the last two might not be. Unix time displays the time in seconds that have elapsed since January 1, 1970. Programmers (and other geeks) are primary users of Unix time. It would be reasonable for the phrase “Internet time” to have you envisioning a clock with the hour and minute hands spinning around wildly, and indeed, I'm wondering why someone hasn't done that. The actual definition of Internet time, however, references Biel Mean Time, which is a global time. Biel Mean Time is the same everywhere in the world, and uses the meridian in Biel, Switzerland, the home of Swatch, as its reference. In other words, with Biel Mean Time, it's the same time everywhere in the world. No more time zones or other arbitrary demarcations of time differences. The day is divided into 1000 beats, so that 1 beat is 1 minute, 26.4 seconds. The current Internet time is shown by the symbol @ plus three digits, ranging from @000 to @999. Thus, a person in Switzerland, a person in Florida, and a person in Hawaii could all hold a conference call at 750 Biel Mean Time, which would be 6 p.m. (local) for the first person, noon EST for the second, and 1 a.m. for the third.

You can also configure whether or not to display seconds (if appropriate), the date, and Universal Coordinated Time (Greenwich Mean Time). You can set the date and time via the Adjust Date & Time menu item in the Clock applet's context menu. You'll need to log in as root in order to do so, because you're changing system properties. Doing so brings forward the Date/Time Properties dialog, as shown in **Figure 38**.

You have two choices: either manually set the date and time, and hope your computer keeps time correctly, or have your computer connect to a remote time server to synchronize with an atomic clock. To do this, select the **Enable Network Time Protocol** check box. You'll need an Internet connection to use this option.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_152_0.png)

**Figure 38.** *The Date/Time Properties dialog allows you to configure how your Clock applet knows what the date and time is.*

In this day and age, it seems everything has a clock: microwaves, VCRs and DVDs, even refrigerators and your sneakers. And as the saying by Robert Anton Wilson goes, “A man with a watch knows what time it is. A man with two is never quite sure.” As a result, knowing that at least *my computer* is accurate is something I like to know.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_153_0.png)

**Figure 39.** The Weather Preferences dialog has two tabs that allow you to configure aspects of the Weather Report applet.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_154_0.png)

**Figure 40.** *The Weather Report applet has three tabs (two shown) that display information about the weather in a selected locale.*

The Current Conditions tab shows a summary of the weather at the location identified in the Preferences, while the Radar Map shows a recent scan of the area in question. The Forecast tab (not shown) is simply a lengthy text description of the weather forecast.

The Weather Report applet is updated as you configured it in the Preferences dialog, but you can force an immediate update by right-clicking the applet's icon and selecting Update from the context menu.

## Summary

Fedora Core offers a nearly unlimited number of methods to customize the interface, and I've just touched on a few ways that I've tweaked my system. Plan on spending some time going through the multitude of options in the various preference dialogs to customize your own desktop, and have it your way!

The purpose of this chapter is to get you started with Linux on your desktop, but of course there's a lot more than what I can cover here. In addition, new versions of Fedora Core are released on a regular basis. I'll keep you up to date on writing new articles as well as posting updates related to this book. These materials can be found on Hentzenwerke's Web site, **www.hentzenwerke.com**. Click “Catalog” and navigate to the page for *Linux Transfer for Windows Power Users*.

# Chapter 6
# Files, Directory Structures, and File Managers

It’s all about data. Your data. Except for those poor souls who wander around airports with a $5,000 notebook that’s used only for Solitaire and the occasional DVD, people use computers to work with data. And oftentimes, that data will be stored on your computer. In this chapter, I’ll discuss what you need to know about dealing with data files on your computer—how files are different on Linux, what the directory structure in Linux looks like and what goes where, and how to manipulate files with popular file managers.

Even in 2004, I’m continually amazed at the disregard that most software manufacturers have toward data. Data is the whole reason we use computers, after all. We’re not spending our time learning software just to learn software—we want to be able to manipulate data with that software. The definition of data spans a wide variety of uses, from word processing documents like letters and proposals, to spreadsheets with this month’s financial projections, to presentations for next week’s sales meetings or group laboratory report, to simply e-mail messages, music files, and pictures of the grandkids.

In a perfect world, your data would just be “there,” and you wouldn’t have to know exactly where “there” was, nor would you need to worry about it; it would always be “there.” Indeed, my personal definition of Nirvana is having all my data accessible to me no matter where I am or what device I happen to have with me at the time.

But the world isn’t quite perfect—yet, at least. So we have to know where our data is, how it’s organized, and how to get to it.

Where do start? This chapter has a “chicken and egg” quality feeling to it. In order to talk about files, you sort of need to have a context for them, such as a directory (or “folder”) structure. But to talk about a directory structure, you sort of need a picture to demonstrate, and what can provide a picture better than a graphical file manager? But a file manager doesn’t do much good without files and directories, so we’re back where we started. So that means you’re going to want to read through this chapter a couple of times. The first time through, I may ask you to take a leap of faith on some things, but the second time through, many of those things will make sense.

## Files: the data itself

A file on a Linux computer is much like a file on a Windows computer, but not necessarily identical. Let’s look at the similarities first.

On Linux, as with Windows, a file can represent a single coherent chunk of data (how’s that for a mouthful?), such as a memo, a spreadsheet, a digital image, a music file, or a database table. You use files for storing data from your application programs as well as for storing the programs themselves.

Now about those differences. First, the naming scheme in Linux is different from Windows. Programs—those files that customarily have an EXE extension—generally don’t have extensions at all. Text files—TXT files—also usually go extensionless. You can create
