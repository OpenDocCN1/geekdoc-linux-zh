![](bbox=[0.11, 0.08, 0.89, 0.63])

Figure 14-9  Workspace Menu and New Subpanel and Action

A couple of things to remember when creating actions: first and foremost, make sure that the PUSH_ACTION and the file names are the same. That similarity is how they find each other. Make sure the that action file ends with .dt and make sure that the description file is executable. If any of these are wrong, the action either won't work or won't appear.

To avoid a lot of typing, sometimes the easiest approach is just to copy an existing definition and insert it where you want your new control to be and then modify it. As you move down the list of control definitions, you're moving from left to right across the front panel (notice that the POSITION_HINTS value increases in each definition). So if you want your new control to be to the right of the date on the front panel, you insert the control on the line below “date” and add a POSITION_HINTS 3 line to your