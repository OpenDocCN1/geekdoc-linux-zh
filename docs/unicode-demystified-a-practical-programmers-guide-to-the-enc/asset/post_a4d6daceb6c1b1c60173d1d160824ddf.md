
# Figure 8-15 Find File window

—and your home directory as the place to start the search. Put in the Named text box of the file you want to search for (you can include wildcard characters) and in the Look in box the directory you want to start the search. The Browse button helps you find the directory you want to start in. Put a check in the Include subdirectories box when you want to search through subdirectories. Click Find to start the search. The part of the window with the fields you just filled in dims as the results are tabulated at the bottom of the window and displayed in the lower half of the window. You can do whatever you want with the found files: copy, move, delete, edit, display, and so on.

Figure 8-15 shows a case-sensitive (page 1459) search for all files whose names end with rc (*rc) in Alex's home directory and all subdirectories. The asterisk matches filenames that begin with a prefix.

In addition to filling in the Name/Location tab, you can click the Date Range tab to specify a date or range of dates the file was created or modified. The default is All files. Put a check in the Find all files created or modified text box to specify a range of dates. In order to be found when you search a range, the file must match the Name/Location criteria and the Date Range criteria.

In addition, you can use the Advanced tab to specify the file type, text within the file, and the relative size of the file. Click Case Sensitive when you want to perform a case-sensitive search for the file you put in the Containing text file.

You can save the results of your search to a file by clicking Save, two buttons below on the right side of the window. You will be given a choice of filename, location, and type of file (text or HTML) you want to save.

# Views II

Views, or subwindows, are key to taking advantage of Konqueror's power. This section covers some of the buttons, indicators, and menu choices that works with your views.

Two indicators are important when you work with more than one view: The Active View indicator and the Link indicator.

Figure 8-16 shows two-by-side views with a terminal emulator below. The toolbar and location bar are side-by-side.

# Active View Indicator

A small circle at the lower-left of each view (Figure 8-16) is green on the active view and white on all others. The active view has the input focus and is the object of all Konqueror menu commands. The location bar displays the location of the file displayed in the active view. Click within a view to make it the active view.

# Konqueror Terminology: View versus Window

The Konqueror window is the entire window with four sides adjacent to the root window, the edge of the workspace, or other windows, usually with a menubar, location bar, and toolbar. The Konqueror window can house multiple views, the term used to describe subwindows within the Konqueror window. In addition to views, Konqueror can have a Navigation panel and a terminal emulator subwindow. Figure 8-16 shows Konqueror with two views and a terminal emulator subwindow.

![](img/aa8214d49e1cf50152c432845129fb3b_349_0.png)

Figure 8-16 Konqueror showing two views and a terminal emulator

# Link Indicator

A small rectangle at the lower-right corner of each view (Figure 8-16) has a small piece of a chain link fence in it in all views that are linked. Two linked views always show the same thing, with a very useful exception, which is covered in the next paragraph. Although linked views display the same information, each may display it differently. For example, one may have an icon view, and the other a detailed list.

# Lock to Current Location/Unlock View

Choose Konqueror menu: Lock to current location to cause the contents of the active view to remain constant, regardless of what links (URLs) you click. With a normal (not locked) view, you click a link, and the view is replaced by the contents of that link. When you have two linked views, neither of which is locked, both views change to reflect the contents of the link. When a locked view is linked to an unlocked view and you click a link in the locked view, the contents of its normal, unlocked link appears in the unlocked view. Click Unlock to return the view to its normal, unlocked state. Refer to the tutorial on page 303.

# Terminal Emulator

When you work locally, a terminal emulator (Window->Show Terminal Emulator) displays the appropriate command each time you change directories graphically in a linked view, helping you to alternate between the graphical interface and the character-based one within a single window.

Table 8-8 shows what to expect when you link various combinations of views, the Navigation panel, and the terminal emulator.

| View and View |
|---|---|
| No link, no lock | Each view displays whatever you click or enter in the location bar while it is the active view. |
| Link, no lock | Both views display the same thing: whatever you click or enter in the location bar while either window is active. |
| Link, no lock | The unlocked view displays whatever you click in the locked or unlocked view or enter in the location bar while it is the active view. The locked view always displays the view that it displayed when you locked it. |

# Links in Views, Navigation Panel, and Terminal Emulator (Continued)

# Navigation Panel and View

No link, no lock

Navigation panel always displays the Navigation panel. The view displays whatever you click in the view or enter in the location bar (it is always the active view).

Link, no lock

Navigation panel always displays the Navigation panel. The view displays whatever you click in the Navigation panel or the view or enter in the location bar (it is always the active view).

Link, no lock

Not very useful. The Navigation panel always displays the Navigation panel; when you lock the view, it always displays the view that you locked it.

# View and Terminal Emulator

No link, no lock

No connection. The view and terminal emulator work independently.

Link, no lock

As long as you are working locally, the working directory of the terminal emulator is always the directory that the view displays.

Link, no lock

Not very useful. When you lock the view, it always displays the same.

# Shortcuts

A shortcut, called a key binding in earlier versions of KDE, is the connection between a key or keys (CONTROL-C, for example) that you hold/press at one time and an action that the system performs when you do. Figure 8-17 shows the Konqueror menubar: Settings->Configure Shortcuts window with the action Copy at the top showing that CONTROL-C is a shortcut for copy and CTRL-Insert is an alternate shortcut. The action Find is highlighted in the figure with a shortcut of CONTROL-F. The bottom portion of the window shows that CONTROL-F is a Custom shortcut. When you highlight copy, you see that CONTROL-D is a Default shortcut.

You can highlight any action and remove a shortcut by selecting the default shortcut (if there is one) by selecting Default. Assign or assign a custom binding by clicking the keycap button (the button with Ctrl-F in Figure 8-17) or the Custom radio button. The Define Shortcut window appears. To specify a

# Konqueror Browser/File Manager 303

| Action | Shortcut | Alternate |
| --- | --- | --- |
| Copy | Ctrl+C | |
| Copy Files | Ctrl+V | |
| Cut | Ctrl+X | Shift+Delete |
| Duplicate Window | Shift+Delete | |
| Edit File Type | Ctrl+D | |
| Forward | Alt+Right | |
| Full Screen Mode | Ctrl+Shift+F | |
| Home URL | Ctrl+F | |
| Konqueror Handbook | | |
| Konqueror introduction | | |
| List View | | |
| Location | | |

Figure 8-17 Configure Konqueror windows

single-key shortcut (clear the Multi-key box if it has a check mark in) and press the key that you want for the shortcut. For a multiple-key shortcut put a check mark in the Multi-key box, press the key combination you want for the shortcut, and click Ok. The names of the keys that are now bound to the highlighted action appear on the keycap button.

The shortcuts that you set in the Konqueror window apply to anything you do within Konqueror. You can set global and application shortcuts (page 321) in a similar manner. The bindings you establish in the Konqueror Shortcuts window take precedence over other bindings.

# Tutorial: Active, Linked, and Locked Views

Open Konqueror, enter www.redhat.com/docs in the location bar, and press RETURN. You may see a Cookie Alert; accept or reject cookies (page 1462) as you please. You should see a single Konqueror view similar to the one shown in Figure 8-16. Because there is only a single view, there is no Active View indicator and no Link indicator. You may want to make the view a little larger by dragging one of the corners.

Choose Red Hat Linux Manuals from the Software drop down menu and click Go. Click x86 installation Guide. You should now see the table of contents for the current Installation Guide.7 Open a second view by selecting Konqueror menubar: Window>Split View Left/Right. You should have two views, each showing the same pane.

+   7. As Red Hat changes its Web site, this page may change. This procedure does not work, try going to www.redhat.com/docs/manuals/linux and selecting the x86 Installation Guide from there.
