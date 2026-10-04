# 4.4 Speed

We’ve tried several methods for extracting a single datum from a mass of data. Now, let’s look at the relative speeds:

![](bbox=[0.134, 0.191, 0.836, 0.458])

# Comparison of Execution Speeds (Tcl8.0p2/BSDI Unix/P166)

The last column in this graph is the combined time that it takes to perform the lsearch and split. Given a set of data that must be split into a list before it can be searched with the lsearch command, an accurate comparison between searching with a regular expression and searching with lsearch should include the time for converting the data to a list.

Regular expressions are very powerful, but slow. Most of the time in a regular expression is used by the regular expression compilation, the setup time. When you can do a single search over an entire string, regular expressions are almost as fast as iterating through a list or converting a string to a list and using search.

The graph was created with the Blt extension. Blt will be discussed in Chapter 13.