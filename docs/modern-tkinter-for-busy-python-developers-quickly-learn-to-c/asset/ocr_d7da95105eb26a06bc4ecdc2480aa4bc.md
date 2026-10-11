All themed widgets carry with them an internal state, which is a series of binary flags. You can set or clear these different flags, as well as check the current setting using the "state" and "instatc" methods. Buttons make use of the "disabled" flag to control whether or not the user can press the button. For example:

```
```text
button.state(['disabled']) ;# set the disabled flag, disabling the button
button.state(['!disabled']) ;# clear the disabled flag
button.instate(['disabled']) ;# return true if the button is disabled, else false
button.instate(['!disabled']) ;# return true if the button is not disabled, else false
button.instate(['!disabled'], cmd) ;# execute 'cmd' if the button is not disabled
```
```

Note that these commands accept an *array* of state flags as their argument.

Using "state"/"inststate" replaces the older "state" configuration option (which took the values "normal" or "disabled"). This configuration option is actually still available in Tk 8.5, but "write-only", which means that changing the option calls the appropriate "state" command, but other changes made using the "state" command are not reflected in the option. This is only for compatibility reasons; you should change your code to use the new state vector.

The full list of state flags available to themed widgets is: "active", "disabled", "focus", "pressed", "selected", "background", "readonly", "alternate", and "invalid". These are described in the themed widget reference; not all states are meaningful for all widgets. It's also possible to get fancy in the "state" and "inststate" methods and specify multiple state flags at the same time.

# ## Checkbutton

+   - Widget Roundup
+   - Reference Manual

A **checkbutton** is like a regular button, except that not only can the user press it, which will invoke a command callback, but it also holds a binary value of some kind (i.e. a toggle). Checkbuttons are used all the time when a user is asked to choose between e.g. two different values for an option.

![](bbox=[0.12, 0.59, 0.9, 0.76])

Checkbuttons are created using the **tk.Checkbutton** function, and typically set up at the same time:

```
```python
measureSystem = StringVar()
check = tk.Checkbutton(parent, text='Use Metric',
                       command=metricChanged, variable=measureSystem,
                       onvalue='metric', offvalue='imperial')
```
```