# 11.3 Building a Megewidget Library

If the option list is a single -option with no associated value, then this procedure will return a list of the values associated with that option for each of the widgets.

If the option list is a set of -option value pairs, then each of the -option value pairs will be applied to each of the subwidgets.

```
Syntax: processOptions optionlist widgetlist ?parent?
```

processOptions Steps through a list of subwidgets, either retrieving the values of configuration options or setting each option in the list to the requested value.

optionlist A list of options and values or a single option to query.

widgetlist The list of subwidgets to process. This list may be full path names (e.g., .parent.megewidget.subwidget) or the subwidget names as returned by makeOptionList.

If the full window path names are used, the parent argument must be unused or an empty string.

If the widgetlist is in the form returned by makeOption-List, the parent argument must be defined.

parent If present, this is the parent widget of the subwidgets.

The processOptions procedure uses the catch command to process the configure subcommand for each of the subwidgets. This allows the script to attempt to set an option on all of the subwidgets without knowing which subwidgets will accept the value and which ones won't. For example, the scrollbar widget accepts a -background option but does not support a -foreground option.

Using the catch is what makes it possible to configure all the subwidgets in a megewidget with a single configure command. This makes the megewidget easier for script writers to use, since they can simply configure the -foreground to a color without needing to know which parts of the megewidget can accept a -foreground option and which ones can't. However,