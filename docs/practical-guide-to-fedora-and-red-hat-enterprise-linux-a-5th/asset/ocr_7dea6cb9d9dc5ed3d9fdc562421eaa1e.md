![](bbox=[0.27, 0.1, 0.81, 0.44])

Figure 24-7  The BIND Configuration GUI window with a right-click menu

# Using this JumpStart

> The system-config-bind utility is a complex tool that you may find helpful for setting up BIND. Run this utility and click Help→Manual on the menubar to display the Fedora/RHEL manual for this utility. Click Help→ISC ARM to display the BIND 9 Administrator Reference Manual. You may want to experiment with this utility after you have set up one of the servers described at the end of this chapter, as its configuration information may make more sense after you go through the process of manually configuring BIND.

This section explains how to use system-config-bind but does not go into detail about what each of the files and settings does. That information is covered in other sections of this chapter.

# Using the BIND Configuration GUI Window

Right-click on an object (line) in the BIND Configuration GUI window to display a pop-up context menu. This menu always has an Edit selection, which displays a window in which you can edit information pertaining to the object you clicked. You can display the same window by double-clicking the object or by highlighting the object and clicking Properties on the toolbar. This pop-up menu also always has an Add selection that displays a submenu with choices appropriate to the object you are working with. Figure 24-7 shows the pop-up menu for the DNS Server object, along with the Add submenu.

In the BIND Configuration GUI window, a triangle at the left end of a line indicates that the object holds other objects. Click a triangle so that it points down to expand an entry. Click it so that it points to the right to collapse an entry.