# Scroll When Mouse Nears Edge

You only need to worry about the feature Scroll when mouse nears edge if you have a situation where your virtual machine's desktop is larger than the VMware window on your Linux desktop. This could happen if you temporarily make the VMware window smaller or if you are using a virtual machine desktop larger than your computer can display (a 1,280x1,024 Windows desktop on a Linux PC whose desktop is only 800x600, for example).

> If you want to be able to change the size of the VMware window on-the-fly, you need to disable Autofit under View on the VMware window settings. Note that this does not affect the size of the Windows desktop itself, just how much you can see at once!

In Figure 8.4, you see a Windows desktop that cannot be fully displayed because the VMware window is too small. With the Scrolling option enabled, VMware automatically pans across the desktop when the mouse nears the edge of the screen. Otherwise, you would need to restore input focus to Linux and drag the window scrollbars to change the visible area of the desktop.

![](bbox=[0.07, 0.65, 0.45, 0.85])

Figure 8.4 Using the Scroll when mouse nears edge feature of VMware Tools, you can pan through a large Windows desktop in a smaller VMware window.

# Hide Cursor

The option Hide cursor is nothing more than a glorified "mouse blanker," but it can help avoid the confusion of seeing two mouse pointers on the same screen. When enabled, the mouse pointer in the Windows virtual machine disappears if the input focus is on Linux rather than VMware.