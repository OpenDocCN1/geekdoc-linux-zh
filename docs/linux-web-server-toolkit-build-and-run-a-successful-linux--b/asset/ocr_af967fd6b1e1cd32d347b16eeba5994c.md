# 262 Linux Web Server Toolkit

![](bbox=[0.165, 0.125, 0.225, 0.175])

If you think you want a user to be able to select more than one of the options listed with your radio buttons, instead use a selection list with the MULTIPLE option. Selection lists are described in the next section.

# SELECTION MENUS

Selection menus, or drop-down selection lists, allow you to provide a user with a list of options to select from. Selection menus differ from other form tags such as radio buttons in two ways. First, the label for a selection menu – the text after each `<OPTION>` tag – is onscreen within the frame. For all other form tags, nothing within the tag is displayed on screen.

Second, selection menus allow users to select more than one item from the list. Selection menus provide several display options that let you control which item is displayed by default and how many items are displayed at once. For example, a selection menu with a height of one item (SIZE= 1 as in Figure 10-7) will appear as a drop-down list. If you define a selection menu with a height of three items (SIZE= 3 as in Figure 10-8), it will appear as a larger box in the browser window with a scroll bar on its right edge. It's important that you test the interface that you create to make certain it's usable. For example, a multiple-selection scrolling list that is only one or two items is difficult to use.

Selection menus begins with a `<SELECT ...>` tag that includes the NAME of the form element, the SIZE (height in items) for the list, and the MULTIPLE option if multiple selections are to be allowed.

Between the opening `<SELECT ...>` tag and the closing `</SELECT>` tag, the `<OPTION>` tag is used. The `<OPTION>` tag is used like the `<li>` tag for HTML lists, simply separating items in the selection list. The only parameter that can be added to the `<OPTION>` is SELECTED, which can be included on one or many items to make them preset. The first option in the next list using the SELECTED parameter, as shown in Figure 10-7.

A sample selection list appears in the following; this example uses a single selection in a drop-down menu format that could replace a set of radio buttons in your:

```
<SELECT NAME= SIZE= 1>
<OPTION SELECTED>UPS Ground
<OPTION>UPS Second Day
<OPTION>Federal Express
</SELECT>
```

The browser display of this simple example is shown in Figure 10-7.