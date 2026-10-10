![](bbox=[0.24, 0.14, 0.54, 0.34])

![](bbox=[0.52, 0.35, 0.77, 0.44])

# Figure 4.6

*The ChangeLog application shows how modifications to a dataset are efficiently stored.*

Note the four lines in the change log. The first line shows the data for a newly added employee. The second line shows the data for a deleted employee. The third and fourth lines show modifications to an existing employee. The third line contains the employee data before any modifications were made, but the fourth line contains data for only those fields that were modified.

# Cloning Data from Another Client Dataset

Client datasets have the unique capability to clone data from another client dataset. When you clone a dataset, there is only one physical copy of the data, but there are two (or more) different datasets accessing the same copy of that data. Changes to one dataset immediately affect the other dataset's view of the data.

Why would you want to do this? I have run into several situations in my projects where cloning provides an elegant solution to an otherwise sticky situation. The following list outlines a few of the benefits:

+   - You can traverse a clone of a dataset without disturbing the original dataset’s current record pointer.
+   - When viewing a dataset in a grid, you can insert a new record in a dialog using data-aware controls that are connected to the clone (without temporarily opening a new, empty line in the grid).
+   - You can apply ranges or filters on the clone without affecting the display of the original dataset.