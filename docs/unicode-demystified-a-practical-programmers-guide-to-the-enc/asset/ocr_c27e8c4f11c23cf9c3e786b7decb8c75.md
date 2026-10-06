# Link Indicator

A small rectangle at the lower-right corner of each view (Figure 8-16) has a small piece of a chain link fence in it in all views that are linked. Two linked views always show the same thing, with a very useful exception, which is covered in the next paragraph. Although linked views display the same information, each may display it differently. For example, one may have an icon view, and the other a detailed list

# Lock to Current Location/Unlock View

Choose Konqueror menu:Lock to current location to cause the contents of the active view to remain constant, regardless of what links (URLs) you click. With a normal (not locked) view, you click a link, and the view is replaced by the contents of that link. When you have two linked views, neither of which is locked, both views change to reflect the contents of the link. When a locked view is linked to an unlocked view and you click a link in the locked view, the contents of its normal, unlocked link appears in the unlocked view. Click Unlock to return the view to its normal, unlocked state. Refer to the tutorial on page 303.

# Terminal Emulator

When you work locally, a terminal emulator (Window->Show Terminal Emulator) displays the appropriate command each time you change directories graphically in a linked view, helping you to alternate between the graphical interface and the character-based one within a single window.

Table 8-8 shows what to expect when you link various combinations of views, the Navigation panel, and the terminal emulator.

| View and View |
|---|---|
| No link, no lock | Each view displays whatever you click or enter in the location bar while it is the active view. |
| Link, no lock | Both views display the same thing: whatever you click or enter in the location bar while either window is active. |
| Link, no lock | The unlocked view displays whatever you click in the locked or unlocked view or enter in the location bar while it is the active view. The locked view always displays the view that it displayed when you locked it. |