![](bbox=[0.14, 0.05, 0.4, 0.2])

+   - Custom Views
+   - Generic Delegates
+   - Representing Tabular Data in Trees

# Advanced Model/View Programming

In the two preceding chapters we explored the basics of PyQt model/view programming.* We saw how to create custom models, and how to use the predefined SQL table models. We also saw how to create custom delegates to control the appearance and editing of data items. In this chapter, we will deepen our knowledge of PyQt model/view programming.

All of the topics covered in this chapter, and the ones that follow, are more advanced than the ones we have seen before, at least conceptually. However, in most cases the code is no more difficult than what we have already seen.

In the first section we will look at how to implement a custom view so that we can see how to visualize our data in any way we want. This section is useful for understanding more about how views work, and to see one straightforward approach to implementing a custom view.

The second section revisits the subject of custom delegates, showing how to minimize code duplication and how to easily create arbitrary delegates for views. This section should prove especially useful to those who need to create many delegates, especially for datasets such as SQL tables where each column is of a particular type.

In the final section we will see how to reflect tabular data into a tree view. One use of this is where we represent tables as trees when the first few columns often contain the same values—this has the effect of reducing the number of rows that the user must navigate to find the item they want. Another use is to let users pick particular values that form a “path”. For example, rather than providing two, three, or more comboboxes, each with values that depend on the current values of its predecessors, we just provide a single tree for the user to navigate and choose from.

> *This chapter assumes a knowledge of PyQt’s model/view architecture, covered in Chapter 14.