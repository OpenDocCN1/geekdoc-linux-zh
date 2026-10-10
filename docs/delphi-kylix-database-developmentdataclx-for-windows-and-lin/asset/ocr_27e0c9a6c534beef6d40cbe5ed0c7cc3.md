The simplest way to use a TDBGrid is to drop it on a form, connect the data source, open the dataset, and then run the application. If you do this, you'll see a fairly mundane grid using all default settings, as shown in Figure 6.2.

![](bbox=[0.26, 0.22, 0.75, 0.46])

Figure 6.2 points out examples of title cells, data cells, indicator cells, and grid background. Using a combination of the grid’s properties and events, you can create a grid that looks much more pleasing to the eye. In the following sections, I’ll examine those properties and events in detail.

# Customizing Columns

Generally, the most basic level of customization that you want to perform is adjusting either the number of columns that are displayed, or the order in which the columns are displayed. TDBGrid published a Columns property, which provides access to the list of columns displayed in the grid.

You can think of the Columns property as being similar to a dataset's Fields property. If there are no columns specifically defined, the grid simply displays all columns in the order that they appear in the dataset. If persistent fields are defined for the dataset, the grid displays columns only for those fields.

To create persistent column objects for the grid (similar to a dataset's persistent field objects), you use the columns editor.