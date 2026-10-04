# 8.4 Determining and Setting Options

-textvariable varName

The name of a variable to associate with this widget. The contents of the variable will reflect the contents of the widget. e.g., the textvariable associated with an entry widget will contain the characters typed into the entry widget.

-width number

The requested width of the widget in pixels.

# 8.4 Determining and Setting Options

The value of an option can be set when a widget is created or can be queried and modified after the widget is created using the cget configure commands.

The cget subcommand will return the value of a widget option.

**Syntax:** widgetName cget option

+   - widgetName: The name of this widget.

+   - cget: Return the value of a single configuration option.

+   - option: The name of the option to return the value of.

The configure subcommand will either return a single configuration option value, return all the configuration options available for a widget, or allow you to set one or more configuration options.

**Syntax:** widgetName configure ?opt1? ?val1? ?opt2? ?val2

+   - widgetName: The widget being set/queried.

+   - configure: Return or set configuration values.

+   - opt1: The first option to set/query.

+   - ?val1?: The value to set for opt1.

If configure is evaluated with no options, then a list of all the available options and values is returned.

217