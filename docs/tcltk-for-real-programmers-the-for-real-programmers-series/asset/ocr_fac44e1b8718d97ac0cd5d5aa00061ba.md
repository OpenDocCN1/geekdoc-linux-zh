# 10.3 Text Widget Subcommands

**Syntax:** textName tag bind tagName ?eventType? ?script?

textName The name of the text widget.

tag bind Bind an action to an event occurring on the tagged section of text, or return the script to be evaluated when an occurs.

tagName The name of the tag that defines the range of characters that will accept an event.

?eventType? If the event field is set, this defines the event that will trigger this action. The event types are the same as those defined for canvas events in Section 9.5.

script The script to evaluate when this event occurs.

The display configuration of text can be modified with the tag configure command. The tag configure command will allow you to set many of the options that control a display, including:

+   -background color The foreground and background colors for the text.
-foreground color

+   -font fontID The font to use when displaying this text.

+   -justify style How to justify text with this tag. May be left, right, or center.

+   -offset pixels The vertical offset in pixels for this line from the base location for displaying text. A positive value raises the text above where it would otherwise be displayed, and a negative value lowers the text. This can be used to display subscripts and superscripts.

+   -lmargin1 pixels The distance from the left and right edges to use as a margin.
-lmargin2 pixels The rmargin value is a distance from the right edge of the text widget to treat as a right margin.
-rmargin pixels