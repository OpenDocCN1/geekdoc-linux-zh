up the console). Furthermore, you'll probably want to substitute your own logo for the penguin, which stops being "cute" after about the third go-around. However, there are no instructions given for this, and that's really moving far beyond the scope of SVGAlib, anyway.

I suggest a strongly worded letter to the GGI maintainers.

# Pseudo Screen Savers

One nifty device you'll find in Windows, Macintosh, and, yes, even the X Windowing System is the *screen saver*. The original concept of the screen saver was to (obviously) save your monitor's screen from burning out. The problem was that back in the old days (and even today, to a lesser extent), if a monitor displayed the same image for a long enough period of time, that image would become permanently etched onto the screen. This was especially prevalent in terminals used for data entry. (If you've ever seen one of these monitors at a garage sale, you know exactly what I mean. There's nothing worse than trying to type when you've got the remnants of some ancient word-processing program obstructing your view.)

To combat this, the screen saver was developed. The concept was simple enough: After a certain period of inactivity, the screen would "blank" itself out. And that was a *true* screen saver. Later on, of course, we had the flying toasters and geometric eye candy that were designed to amuse more than they were ever intended to prevent burn-in.

As you probably know, Linux has the basic screen-blanking facility built into the kernel. This is accessed with a simple command, such as the following:

```
```
/bin/setterm -blank 15
```
```

With that, your screen will go blank after 15 minutes of inactivity. The actual code to make it happen is contained in /usr/src/linux/drivers/char/console.c.

Don't go hacking that file just yet, though. Any attempt to execute an SVGAlib program there will crash your system, for the same reasons that you have to use ifbcon to show graphics on startup (the kernel's in protected mode). You'll get colors on your screen, all right, but probably not the ones you want.

I'm not about to go into the intricacies of integrating a screen saver into your kernel (for the same reasons I cut short my discussion on boot-time graphics), but I will show you how to make a "fake" screen saver. (Fake, you say? What's the problem?) Well, it's fake because you have to start it yourself.

Bear with me. The fake screen saver (or self-displaying graphic) is an excellent vehicle to start learning about netpbm (pbm stands for Portable Pixmap). Netpbm is an improvement on the original pbmpls package, created by Jef Poskanzer, and is filled with tons of