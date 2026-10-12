enables you to use the graphical login upon bootup rather than logging in at the command line. Or you can choose to skip configuring X altogether if the box is too slow, does not have enough memory or drive space, or will not require X for the tasks it will perform.

I prefer customizing X to my own specifications while skipping the graphical login. The Customize page allows for varying levels of resolution and pixel bits. Depending on the make of your video card and the model of your monitor, the settings shown in the following table can vary somewhat. With the latest Red Hat Linux release, all the options are already selected, and when you test the configuration it will attempt to display the highest range. Here is a break down of the settings for a generic 4 megabyte video card:

8 Bits per Pixel 16 Bits per Pixel 32 Bits per Pixel

640 × 480 640 × 480 640 × 480

800 × 600 800 × 600 800 × 600

1,024 × 768 1,024 × 768 1,024 × 768

1,152 × 864 1,152 × 864 1,152 × 864

1,280 × 1,024 1,280 × 1,024 1,280 × 1,024

1,600 × 1,200 1,600 × 1,200

I have found that the 16 bits-per-pixel rate set at 1,024 × 768 suffices on most all video cards to provide the needed color and resolution. This setting is also the recommended setting for 15-inch monitors and greater. These higher settings are recommended only if you have a monitor of 17 inches or greater; otherwise the fonts might be too small to be easily readable. Also, higher pixel settings will require more time to render the image. Higher resolutions will lower the color depth, and so it becomes a trade-off between higher resolution or increased color depth. Eight-bit settings will allow only as many as 256 colors. This is fine for simple console usage, but when you are running a higher-end monitor with graphics-intensive programs, usually 16 bits is the preferred setting. You can use 32-bit resolution for high-end graphics work or for gaming on Linux.

While still in the Red Hat install routine, you can test the settings chosen to verify their correctness and to see whether the monitor and card will display images correctly. If an image or graphic does not appear in the test, you will be informed