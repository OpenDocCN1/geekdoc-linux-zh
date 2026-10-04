# 11.7 A Different Technique for Building Megawidgets

| frame | Return a frame that can be displayed with one of the layout managers (pack, place, or grid). |
 tolevel | Return a top-level window that can be displayed outside the application window. |
 components list | The components of this megawidget. Each component is defined in a list with these fields: |
 type | The type of widget will be: button, label, etc. |
 name | The name for this widget. |\ args | A list of arguments that will be appended to the widget creation line when this widget is created. This is where arguments defining the relationship between a scrollbar and its target widget can be placed. |

The next example creates a megawidget that consists of a prompt and an entry widget. By default, the prompt will be on the left of the entry widget, but it can be configured to be on the right (to demonstrate using the configure command).