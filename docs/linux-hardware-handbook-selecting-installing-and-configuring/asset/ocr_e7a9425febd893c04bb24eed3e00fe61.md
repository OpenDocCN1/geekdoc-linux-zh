It's important to realize that OpenGL support for a video card is independent of X support for the same video card. A card might have very good 2D support in XFree86, Accelerated-X, or Metro-X, for instance, and have excellent 3D hardware, and yet have no OpenGL 3D support. Therefore, if 3D acceleration is important to you, it's vital that you check for support in both XFree86 (or a commercial X server) and your OpenGL implementation of choice.

# ## Video RAM

In order to display an image on a monitor, a computer needs to provide a steady stream of information to the screen. Most monitors today have a *refresh rate* in the *70Hz-100Hz* range at the resolutions at which the monitor is used, which means the monitor's display is completely redrawn *70-100* times per second. The video card must be able to provide a constant stream of data to the monitor. Consequently, the video card must have continuous access to the current image of the display. One of the reasons video cards exist at all is so that the video card can serve as a buffer between the computer and the monitor. Rather than deal with the logistical nightmare of providing access to a single image to both the computer's CPU and the video hardware, the video card serves as an intermediary between two banks of memory, as shown in Figure 12.3.

![](bbox=[0.18, 0.51, 0.72, 0.65])

**Figure 12.3**  
One of the functions of a video card is to create a pool of RAM apart from the system RAM in order to isolate the system RAM from video display-timing requirements.

This design leads to the need to consider a video card's RAM separately from the RAM used on a computer's motherboard. Using a video card with inadequate RAM can restrict the availability of high-resolution or high-color-depth video modes. Different video cards also support different types of video RAM, which vary in their speed characteristics, just as different types of motherboard RAM do.