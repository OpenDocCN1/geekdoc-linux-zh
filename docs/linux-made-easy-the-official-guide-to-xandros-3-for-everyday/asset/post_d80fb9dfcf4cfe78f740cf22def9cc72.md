
## FLATBED MEMORIES
*Working with Your Scanner*

![](img/3badae5570de77b990135448f8a8a1cc_188_0.png)

Scanners are both extremely useful and about as cheap a peripheral device as you can get. They allow you to take either images or pages of text and input them in digital form into your computer in much the same way as you duplicate a document on a copy machine. However, even as digital cameras are rapidly overtaking traditional film cameras as the photographic device of choice for the masses, the number of people using scanners to transfer their non-digital images into digital form is slowly decreasing. Despite this trend, scanners are not in immediate danger of extinction because there are more images around than those you take yourself.

Even though scanners have been around for a relatively long time, support for them in Linux is still a bit spotty. Fortunately, this is changing for the better with every new Linux release. The *backend*, the essentially hidden part of your system that handles scanner recognition and support in Linux, is called *Sane*. If you are wondering whether Linux will be able to recognize your scanner, or if you are trying to figure out what type of scanner to buy, you will probably want to go to the Sane website, www.sane-project.org/sane-mfgs.html.

There you will be able to see if your scanner is supported or to get tips as to what scanner to buy. As I have mentioned before, you can also try out the Xandros User Forums (http://forums.xandros.com) and ask for Xandros-specific recommendations there.

### Project 10A: Scanning

For those of you who have a scanner, now is the time to get a feel for how to use it with Xandros by following along with this project. To get started, make sure your scanner is plugged into your computer and turned on.

After that, here’s what you have to do:

1. Go to the **Launch** menu and select **Applications** > **Graphics** > **Scanner**. This will launch the scanning application known as *Kooka*.
2. The Kooka Welcome window (Figure 10-1) tells you which scanning devices you have connected to your machine and asks you to pick one. Assuming you have only one, just click **OK**.

![](img/3badae5570de77b990135448f8a8a1cc_189_0.png)

Figure 10-1: The Kooka Welcome window

> **NOTE**
> *If the scanner you are using is the only one you are likely to connect to your machine in the near future, then go ahead and check the box next to the words Do not ask on startup again, always use this device, which will allow you to bypass this phase of the startup in the future. If you do happen to add, or switch, scanners in the future, you will be able to make the appropriate changes in the Kooka Preferences window at that time. Once you click OK, the main Kooka window will appear.*

Now that Kooka is up and running, you can get down to some scanning. The first thing we’ll do is perform a preview scan. This is a quick, low-resolution scan, which allows you to see a thumbnail, a small version of the image you will be working with.

3. Choose a photo you would like to scan, place it on the scanner bed, and then close the cover.
4. Click the **Preview Scan** button in the main Kooka window, after which a small window (Figure 10-2) will appear showing you the progress of the scan.

![](img/3badae5570de77b990135448f8a8a1cc_190_0.png)

Figure 10-2: Kooka shows your scanner's progress

Once your scanner has finished doing its thing, the progress window will disappear, and you will see a thumbnail of your image in the right pane of the main Kooka window, which at that point should look like Figure 10-3, though your preview image will (unless we move in surprisingly similar circles) be different.

![](img/3badae5570de77b990135448f8a8a1cc_190_1.png)

Figure 10-3: The main Kooka window after performing a preview scan

After the thumbnail preview of your image appears, you must select the part of it you want to scan. This can be a very handy feature, as it allows you to perform some after-the-fact digital magic. Imagine, for example, that you have a killer photo of yourself that you want to include in a digital photo album. The only problem is that standing at your side in that photo is your ex, Chris, who, given the course of things in your life, you would rather place squarely into the trash bin of your memory.

Of course, rather than stave off a bout of heartbreak by removing your ex, you might, as is the case with my happily married friend in Figure 10-4, just want to isolate a portion of a photo for use as a headshot in a web page or on a letterhead.

Even if you have no need to erase or isolate someone in your image, and you instead want to scan the whole image, you still have to make a selection, in this case from image border to image border. If you don't do this, your scanner, not knowing any better, will scan the entire area of its scanning bed, thus producing an image with an enormous amount of empty white space. In all likelihood, this is something you want to end up with about as much as eggshells in your omelet.

![](img/3badae5570de77b990135448f8a8a1cc_191_0.png)

*Figure 10-4: Selecting the portion of the image you want to scan*

5. To make the selection, place your cursor at one corner of the image or part of the image you want to scan (the cursor’s shape will change from the traditional arrow to a crosshair), press and hold down your left mouse button, and then drag the cursor until you have surrounded the area you want to scan with the dashed selection box (sometimes referred to as “marching ants”) that then appears (Figure 10-4). Release the mouse button.

If you are selecting only a relatively small area of an image, as in the example we’re using, it would behoove you to increase, perhaps by twice, the resolution so as to end up with a clearer final image. You can adjust resolution settings by using either the slider or the up arrow in the main Kooka window next to the word Resolution (Figure 10-5).

![](img/3badae5570de77b990135448f8a8a1cc_191_1.png)

*Figure 10-5: Changing the resolution for the final scanned image*

6. Now that you have selected the area you want to scan, click the **Final Scan** button to seal the deal.

A progress window like the one you saw during the preview-scan phase of things will appear again, and, after your scanner spouts out a few tugging sounds, you will hear the long, steady hum of your scanner doing its job. During this time the progress bar will begin its mercurial journey to completion. When the scan is indeed complete, the progress window will disappear, and a Kooka Save Assistant window (Figure 10-6) will open in its place.

![](img/3badae5570de77b990135448f8a8a1cc_192_0.png)

7. Choose a format in which to save your image (I use *JPEG* for images I will use on a web page and *PNG* for everything else), and click **OK**.

### Viewing the Results

To see the results of your final scan, you will need to move your mouse over to the right pane of the main Kooka window (Figure 10-3), and then click the tab showing an icon of a folder and file. Since this might be a bit hard to make out, I’ve highlighted it for you in Figure 10-7.

![](img/3badae5570de77b990135448f8a8a1cc_192_1.png)

Once you click that tab, the results of your final scan will appear in the right pane of the main Kooka window, as you can see in Figure 10-8.

You will also notice that a thumbnail of the image will appear at the bottom of the pane and that the default filename for that file will be listed in the left pane (in this case, *kscan_0001.png*).

![](img/3badae5570de77b990135448f8a8a1cc_193_0.png)

Figure 10-8: The final result of your scanning efforts

### Getting a Fuller View

Of course, especially when dealing with larger images or images scanned at much higher resolutions, most often only a part of your final image will be visible in the right pane, as you can see in the left part of Figure 10-9. This is simply because the final image is too big to fit in the relatively small area provided in the Kooka window.

![](img/3badae5570de77b990135448f8a8a1cc_193_1.png)

Figure 10-9: Viewing a scanned image before and after scaling
