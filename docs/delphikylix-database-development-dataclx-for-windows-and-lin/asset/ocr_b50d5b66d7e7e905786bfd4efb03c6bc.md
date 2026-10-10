DisableStringTrim is a global property, in that it affects all the string fields in the dataset. It doesn't allow you to trim trailing spaces from the FirstName field, and still retain trailing spaces for the LastName field. If you want to retain trailing spaces for some fields and remove them for others, you need to set DisableStringTrim to True, and then remove trailing spaces manually from the appropriate fields (perhaps in the dataset's BeforePost event handler).

# ReadOnly

By default, client datasets are read/write datasets. You can make a client dataset read-only (if the underlying data is stored on a CD-ROM drive, for instance) by setting the dataset's ReadOnly property to True.

# Summary

In addition to the basic functionality presented in the preceding chapter, TClientDataSet supports a number of advanced operations. In this chapter, you learned the following:

+   - Datasets provide a number of events that you can hook into and be notified when certain operations occur. In addition, you can raise an exception during the Beforexx events to prevent the operations from occurring.
+   - You can increase performance dramatically by disabling data-aware controls during lengthy processes.
+   - Delphi datasets provide support for BLOBs, which can be used to store notes, images, and other unformatted data.
+   - Nested datasets provide simplified master/detail support in client datasets.
+   - TClientDataSet's undo support enables you to perform what-if scenarios in your applications.
+   - By cloning a client dataset, you can perform operations on a clone of the data without disturbing the settings of the original dataset.
+   - Maintained aggregates support the automatic calculation of sums, minimums, maximums, counts, and averages for groups of records or for the entire dataset.

The following chapter begins a two-chapter introduction to data-aware components.