
guessed right—Winamp skins and XMMS skins are interchangeable. Just be *sure* *not* to use those skins designed for Winamp 3, which will not work. You can tell which are which by the file extensions: Winamp 3 skins end in .wal, Winamp 2 skins (the XMMS compatibles) end in .zip, and native XMMS skins end in .wsz.

There is an amazing variety of skins available from the Winamp site, so there should be something there to please you. When you find some skins that you like, download them in the usual manner.

## 14B-3: Installing Your New Skins

Once you have downloaded some new skins, you will have to make them available to XMMS by putting them in the right place on your system. You needn't unzip them, though; you can use them as is, which saves you some minor grief. Anyway, at this stage of the game, this is most easily done by putting them in the .xmms folder within your Home folder.

Directories preceded by a dot are normally hidden from view, so to locate the .xmms folder, you will need to go to the **View** menu in a Xandros File Manager window and select **Show Hidden Files**. If you are going to be accessing the XMMS Skins folder often, this would be a good time to use XF*MS*'s bookmark function, so as to make navigating back to the folder easier in the future.

From there on in, it's a simple drag-and-drop procedure. Just drag the downloaded skin files directly into the Skins folder inside .xmms, and that's it. The next time you open the XMMS Skin selector, your new skins will be there waiting in the list.

## Project 14C: XMMS Plug-Ins

XMMS not only allows you to change its looks through the use of skins, but it also allows you to add various functions to the player through the use of *plug-ins*. Many of these plug-ins are already bundled with your system, while still others are available from Xandros Networks. There is a variety of such plug-ins, and they range in function from visualization modules (which provide you with animated graphical representations of the song you happen to be playing) to timer functions (which allow you to have XMMS start up and shut down, like an alarm clock, when you want).

### 14C-1: Using What You've Got

Many of the plug-ins you already have on your system are enabled by default in order to allow XMMS to do what it needs to do. To use the other, less-necessary plug-ins, however, you will need to enable them yourself. Let's start out by taking a look at one of the simplest, called *On Screen Display*, which displays the details of the song you are playing on your screen outside the XMMS player itself (Figure 14-19).

![](img/3badae5570de77b990135448f8a8a1cc_289_0.png)

*Figure 14.19: Song details displayed on-screen with the XMMS On Screen Display plug-in*

To enable the plug-in, follow these steps:

- 1. Right-click any of the XMMS components, and select **Options Preferences** in the pop-up menu that appears.
- 2. When the XMMS Preferences window appears, click the **General Plugins** tab.
- 3. In the General Plugins tab, select the **On Screen Display** plug-in by clicking it once.
- 4. Next, check the *Enable plugin* box at the bottom-right corner of the window (Figure 14-20), and then click the **Apply** button. If you then play a song in XMMS, the artist, track number (within the playlist), and song title will appear in green at the bottom-left corner of your screen for three seconds.

![](img/3badae5570de77b990135448f8a8a1cc_289_1.png)

All very cool . . . but green? And so small? And only three seconds? Fortunately, it is possible to configure most plug-ins to suit your own needs and desires. When you select a plug-in, the Configure button below the list of plug-ins list will become active (clickable) if that plug-in is configurable, as is the case with the On Screen Display plug-in.

### 14C-2: Changing the Display-Duration and Color Settings

To get a feel for how this works, let’s change the behavior of this particular plug-in by doing the following:

- 1. Select **On Screen Display** in the plug-in list (if you haven’t already done so) by clicking it once.
- 2. Next, click the **Configure** button, which will bring up the Configuration window for the On Screen Display plug-in (Figure 14-21); the options within the Configuration window for other plug-ins will, of course, be different.

![](img/3badae5570de77b990135448f8a8a1cc_290_0.png)

- 3. In that window, increase the amount of time the song information will appear on-screen by clicking the up arrow to the right of the word *Timeout* until the appropriate number of seconds is displayed in the box to the left of the arrows (I have mine at 20).
- 4. Once you have set the display time, click **Apply**.
- 5. To change the color of the onscreen display, click the **Set** button to the far right of the word *Colour*, and a color-selection window (Figure 14-22) will appear.

![](img/3badae5570de77b990135448f8a8a1cc_291_0.png)

Figure 14-22: Changing the color of the onscreen text displayed by the On Screen Display plug-in

- 6. In the color wheel, click the color in which you would like your onscreen text to appear. You can then fine-tune your selection by clicking within the color bar to the right of the wheel.
- 7. Once you have made your selection, click the **OK** button, and that window will disappear. You can then go ahead and click the **Apply** button in the Configuration window to complete this part of the process.

### 14C-3: Changing the Display Font and Onscreen Position

Now that you’ve gotten the display font and color taken care of, wrap things up by changing both the font and text size of the display, so as to make it all easier to see. Then change the onscreen location where it will be displayed. While still in the Configuration window, follow these steps:

- 1. Click the **Set** button at the far right of the *Font* row, to bring up the XOSD (X On Screen Display) Font window.
- 2. In the list of fonts in the left pane of the window, scroll down and select **helvetica** by clicking it once.
  > You will now notice that just below the preview pane at the bottom of the window the following message will appear: *This is a 2-byte font and may not be displayed correctly*. Well, we certainly don’t want anything that may not be displayed correctly, so it’s best to change your selection a bit.
- 3. Scroll down a bit in the middle pane, and select **bold** just below the *iso8859-15* heading.
- 4. Once you’ve done that, click the small diamond-shaped **Points** button next to the word *Metric*.
- 5. Now select **24\*** in the *Size* pane on the right side of the window.
- 6. Your font-selection window should now look like that in Figure 14-23. Assuming it does, click the OK button.

![](img/3badae5570de77b990135448f8a8a1cc_292_0.png)

- 7. This will bring you back to the Configuration window, where you should then click Apply.
- 8. To wrap things up, change the position of where the song information is displayed on-screen by using the set of arrow buttons that looks something like the navigation controls of the remote control unit for a DVD player (Figure 4-21). Just choose the position you prefer by clicking the appropriate arrow button.
- 9. Once you have made your selection, click Apply.

### 14C-4: Viewing Your Results

After you have finished the configuration process, go ahead and close the Preferences window by clicking OK. In order to see the results of your efforts, play a tune or two in XMMS (or stop whatever tune you have playing, and then click the Play button again). The song information for the tune you are currently playing will then appear in its new color and font configuration at a new location on your screen.

### Playing Around with Other Plug-Ins

If you are excited by this plug-in business, you might want to try out some of the other plug-ins listed in various tabs of the Preferences window. The visualization plug-ins are always pleasant enough, as are the echo plug-ins, so you might want to try those. If you would like to download and install some other plug-ins via Xandros Networks, try xmms-alarm and xmms-goodnight, which allow you to start up and shut down XMMS automatically at the times you specify.
