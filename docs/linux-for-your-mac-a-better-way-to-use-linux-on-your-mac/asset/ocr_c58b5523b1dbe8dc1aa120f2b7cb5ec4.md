# 192  Chapter 9: Connecting to the Internet

![](bbox=[0.15, 0.07, 0.65, 0.4])

Figure 9.12 Use Netscape's Preferences dialog box to customize many different features of Communicator.

Customizing Netscape is accomplished at least two ways. The first is to use the Preferences menu item found under the Edit menu. The Preferences dialog box (shown in Figure 9.12), offers many different ways to change the way Netscape works.

Click on the drop-down menus along the left-hand side of the dialog box and the right-hand side will change in order to offer new choices. Another way to maximize screen real estate and get the most out of your browser window is to use the Appearance preferences dialog box (shown in Figure 9.12) and then select Text only for the Toolbar. You can also use Navigator's View menu (while browsing) to remove any unwanted menus. This will provide the largest maximum window area for browser information.

Another way to customize Netscape is to edit its X resources. Navigator's resources are text strings that can be used to customize default window sizes, colors, and even how Navigator reacts to keyboard and mouse pointer events. For example, if you have a USB three-button mouse with a middle mouse button that is also a scroll wheel, use the following resource settings:

```
!## NETSCAPE

Netscape*drawingArea.translation: #replace \\
<Button1Down>: ArmLink() \n\
<Button2Down>: ArmLink() \n\
-Shift<Btn1Up>: ActivateLink() \n
```