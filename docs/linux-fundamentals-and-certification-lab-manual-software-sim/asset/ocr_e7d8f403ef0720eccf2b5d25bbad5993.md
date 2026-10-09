![](bbox=[0.27, 0.08, 0.67, 0.36])

# FIGURE 9–1
Video chipset.

During video configuration you may be presented with a list of choices. The driver you select should match your chipset. If you are not sure, power off the computer and remove the video card for a visual inspection. If the video is built in, visual inspection of the main board is required. Many different chipsets are on the board, but the video chipset is usually one of the largest. If you are unsure of the chipset, you can try the generic video drivers.

A simple way to identify the video device type is to observe the BIOS messages displayed following a system reset. Often the video card will display its manufacturer and model along with additional details.

One last way to determine the video driver is to inspect it with a machine or which it is already installed and running. For example, on a Linux installation you can view the /usr/X11/lib/X11/XF86Config file (Figure 9–2) for the Section “Device”, which will list the video adapter driver, vendor name, and board name.

![](bbox=[0.27, 0.62, 0.82, 0.88])

# FIGURE 9–2
XF86Config file.

On a Windows-based installation you can view the video information on the Device Manager (Figure 9–3).