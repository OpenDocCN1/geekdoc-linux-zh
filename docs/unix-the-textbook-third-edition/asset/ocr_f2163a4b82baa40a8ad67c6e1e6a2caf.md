The main part of the buffer in Figure 3.20 shows the “Emacs” customization group, which contains several other subgroups (“Editing,” “Convenience,” etc.). The contents of those subgroups are shown in the single line of description for each group.

The state of the group indicates whether the settings in that group have been edited, set or saved.

Most of the customization buffer cannot be changed, but it includes many editable fields. For example, at the top of the customization buffer is an editable field for searching for settings, with a Search button next to it. There are also buttons and links that you can activate by either clicking with the mouse, or moving the point there and then pressing <Enter>. For example, group names like “[Editing]” are links; activating one of these links brings up another customization buffer for that group.

In any particular customization buffer, you can type <Tab> (widget-forward) to move forward to the next button or editable field. <Shift+Tab> (widget-backward) moves back to the previous button or editable field.

# 3.3.13.2.1 Browsing and Searching for Settings:

From the top-level customization buffer created by <Alt+X> customize, you can follow the links to the subgroups of the “Emacs” customization group. These subgroups may contain settings for you to customize; they may also contain further subgroups, dealing with yet more specialized subsystems of emacs. As you graphically navigate the hierarchy of customization groups, you will find some settings that you want to customize according to your own personal preferences, and according to the nature of the text documents that you are efficiently trying to edit.

# 3.3.13.2.2 Changing a Variable:

Here is an example of what a variable, or user option, looks like in a specific customization buffer. This variable is accessed by descending down from the top emacs group through the groups Editing>Killing, and then left-clicking on the small diamond shape pointing toward the text Kill Ring Max:

```
Kill Ring Max: 60
[State]: STANDARD.
Maximum length of kill ring before oldest elements are thrown away.
```

The first line shows that the variable is named kill-ring-max, formatted as Kill Ring Max for easier viewing. Its value is 60. On our graphical display, the line after the variable name indicates the customization state of the variable; in this example, STANDARD means you have not changed the variable, so its value is the default one. The [State] button gives a menu of operations for customizing the variable.

Below the customization state is the documentation for the variable. To enter a new value for Kill Ring Max, just click to the right of the value and edit it. As you begin to alter the text, the [State] line will change to:

```
[State]: EDITED, shown value does not take effect until you set or save it.
```