optional "length". You should also define the range of the number that the scale allows users to choose; to do this, set a floating point number for each of the "from" and "to" configuration options.

There are several different ways you can set the current value of the scale (which must be a floating point value between the "from" and "to" values). You can set (or read, to get the current value) the scale's "value" configuration option. You can link the scale to a variable using the "variable" option. Or, you can call the scale's "set value" method to change the value, or the "get" method to read the current value.

There is a "command" configuration option, which lets you specify a script to call whenever the scale is changed. Tk will automatically append the current value of the scale as a parameter each time it invokes this script (we saw a similar thing with extra parameters being added to scrollbar callbacks and those on the widgets they scroll).

As with other themed widgets, you can use the "state disabled", "state !disabled" and "!nstate disabled" methods if you wish to prevent the user from modifying the scale.

*As the scale widget does not display the actual values, you may want to add those as labels.*

# ## Spinbox

+   •Widget Roundup
+   •Reference Manual

A **spinbox** widget allows users to choose numbers (or in fact, items from an arbitrary list). It does this by combining an entry-like widget showing the current value with a pair of small up/down arrows which can be used to step through the range of possible choices.

Spinboxes are part of the classic Tk widgets; there is not presently a spinbox in the themed Tk widget set.

![](bbox=[0.12, 0.58, 0.88, 0.72])

Spinbox widgets are created using the **Spinbox** function:

```
```python
spintval = StringVar()
s = Spinbox(parent, from_=1.0, to=100.0, textvariable=spintval)
```
```

Like scale widgets, spinboxes are normally used to let the user choose a number between a certain range (specified using the "from" and "to" configuration options), though through a very different user interface. You can also specify a "increment", which controls how much the value changes everytime you click the up or down button.

Like a listbox or combobox, spinboxes can also be used to let the user choose an item from an arbitrary list of strings; these can be specified using the "values" configuration option, which works in the same was as in comboboxes. Specifying a list of values will override to "from" and "to" settings.

*You might be puzzled about when to choose a scale, listbox, combobox, entry or a spinbox, since usually several of these can be used for the same types of data. The answer really depends on the type of data you want the user to select, platform user interface conventions, and the role the value plays in your user interface.*