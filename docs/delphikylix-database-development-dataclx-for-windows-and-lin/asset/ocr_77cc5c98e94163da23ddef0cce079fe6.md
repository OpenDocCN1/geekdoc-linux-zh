![](bbox=[0.27, 0.12, 0.6, 0.32])

# FIGURE 3.9
Search demonstrates indexed and nonindexed searches.

# Summary

TClientDataSet is an extremely powerful in-memory dataset that supports a number of high-performance sorting and searching operations. Following are several key points to take away from this chapter:

+   - You can create client datasets both at design-time and at runtime. This chapter showed how to save them to a disk for use in single-tier database applications.
+   - The three basic ways of populating a client dataset are
+     - Manually with *Append* or *Insert*
+     - From another dataset
+     - From a file or stream (that is, via persisting client datasets)
+   - Datasets in Delphi can be navigated in a variety of ways: sequentially, via bookmarks, and via record numbers.
+   - You can create indexes on a dataset enabling you to quickly and easily sort the records in a given order, and to locate records that match a certain criteria.
+   - Filters and ranges can be used to limit the amount of data that is visible in the dataset. Ranges are useful when the relevant data is stored in a consecutive sequence of records. Unlike ranges, filters do not require an index to be set before applying them.
+   - *Locate* and *Lookup* are nonindexed search techniques for locating a specific record in a client dataset. *FindKey*, *FindNearest*, *GotoKey*, and *GotoNearest* are indexed search techniques.

In the following chapter, I’ll discuss more advanced client dataset functionality.