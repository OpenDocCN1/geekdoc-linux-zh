# 16.2 Setting Up X

Next is the monitor configuration section. This is where you need to know the horizontal sync range. There are nine predefined monitors you can choose from, and a tenth allows you to define your own range.

**WARNING:** Be sure that the numbers entered here are correct, because a wrong monitor and video card pair can damage your monitor, video card, or both. Don't say I didn't warn you.

Next is the vertical sync. Here you have a choice of about four monitor types, plus one to let you define your own. Once the vertical is set, you can enter information about your monitor. This section isn't necessary, as it allows XFree86 to use multiple monitors at the same time. You can either press enter and use the default for each, or enter a unique identifier for your monitor, along with a vendor name and model name.

Once this is completed, you set up the video card. It's important to select the correct video card because two video cards from the same vendor can have very hardware internally. Selecting the wrong card can damage your card or monitor.

Now you get to select the type of video to run. If you selected a video card that has an accelerator chip supported by XFree86, you'll be able to select that X server.

The options are as follows:

+   1. The XF86_Mono server, which is a 640x480 resolution with two colors, black and white. This should work for all VGA cards. If you suspect a problem with your video card or are unsure of the type of video card you have, this may be a good starting point.
2. XF86_VGA16 server, which is also 640x480, but with 16 colors. This should also work with all VGA-compatible cards.
3. XF86_SVGA server, which provides Super VGA (SVGA) resolutions with 256 colors. This is an accelerated server, so most ISA SVGA cards will probably work with it.
4. Accelerated server, which is for accelerated cards. This gives more than 256 colors for most servers, and higher resolutions. These servers also utilize any of the fastest chipsets in most modern video cards.
5. The server for the video card you selected earlier.

If you select 5, the best server for your card is set up for installation. Now you must get information about your video card. First you'll be asked about the amount of video memory on your card. You'll get five