# Chapter 16 • X Windowing System

selections from 256K to 4096K (4 Mb) and a sixth selection that allows you to enter your own amount.

Once that is completed, you'll be allowed to enter a description for your video card similar to the monitor descriptions above. You can either enter through the entries, or type in the description, vendor, and model of your video card.

If you have an S3- or AGX-based video card, you may need to know the type of random access memory digital to analog converter (RAMDAC) the card has. The RAMDAC is used to get high color (greater than 32K colors) from the server. Enter the appropriate entry if you have those cards and know the RAMDAC type, or else you just press enter.

Some video cards also have a programmable clock. Some clocks are programmable, but if yours is (some Diamond cards and S3 cards are), enter the type of clockchip you have. It should be found in your owner's manual, or on the card itself. If you don't have a clockchip, just press enter.

At this point, the x86config program will attempt to find the clocks your card supports by using the X -probe command. This command doesn't start X itself, but asks the video card to return what clocks it knows about. These clocks are important to determine the correct resolutions you use.

Now you should be ready to start X. Doing this is simply getting to a command prompt and typing

```
> startx
```

This will start the X server in the lowest color depth and resolution you selected. If you configured your server to use 8-bit color (256 colors) and also for 16-bit (65K colors), just typing startxs will start the X server in 8-bit mode. To start it up in 16-bit mode, use the following:

```
> startx --bbpp 16
```

For the sake of extra memory, you may want to log out of other virtual consoles (VCs) before starting X, since you can start multiple shells (xterms) from within X. You can switch to a virtual console while in X by pressing CTRL-ALT-Fn where n is a number between 1 and 6. The first X usually uses virtual console 7. You can see what VC is being used when X starts up, or by going through the virtual consoles.