# 11.3 Building a Megawidget Library

This section will show how to create a library of procedures to manipulate the options for a megawidget. In Section 11.4 we'll use this library to build a scrollable listbox megawidget.

+   - A configuration option can be defined for the entire megawidget and it will be propagated to all appropriate subwidgets.

+   - A configuration option can be defined for a list of subwidgets by declaring those subwidgets in a configure command.

+   - A subwidget is identified by its window name. This may be a complete window path or just the final entity of the window path. For example, .parentwindow.megawidget, .subwidget.megawidget.subwidget may be identified as .parentwindow.megawidget.subwidget or .subwidget or subwidget

+   - Subwidgets may begin with "," but the "_ is not required.

The procedures that implement these conventions are created within a namespace, and all the procedure names are exported. Thus, megawidget that use this library may import the commands into their namespace.

Two procedures are defined in this library: makeOptionList and processOptions. The makeOptionList procedure messages its input into a set of lists that the processOptions procedure can iterate through to set options in the subwidgets.

The makeOptionList procedure takes a list of arguments in the form
?subwidget1? ... ?subwidgetN? -option1 ?value? ... \
?-optionN valueN

and splits into a list of subwidgets and a list of options. The contents of the subwidget list are checked against a list of valid subwidgets, and only valid subwidget names are placed in the list of subwidgets to be returned. If there are no valid subwidgets in the argument list, the procedure will return a subwidget list that contains all valid subwidgets.

Returning a list with all the valid subwidgets when no subwidgets is requested is perhaps not intuitive. This behavior allows all of the subwidgets to be modified when the megawidget configure command is invoked with no subwidget list.