# References

![](bbox=[0.163, 0.121, 0.767, 0.403])

FIGURE 11.6

Sysprof's GTK interface.

represent calls from that function. Double-clicking on a node will update the related Functions and Callers views, based on the selected node.

The Functions views display a sorted list of the functions that consumed the most time. By default, the Functions view sorts based on the total time, which highlights the hottest call chains. Sorting this view by time highlights the most expensive functions in the profile. Single-clicking on an element of the Functions view will update the Descendants and Callers views, with the call stack information for that element.

Finally, the Callers view displays the call sites for the highlighted function, i.e., where the current function was called from, and the percentage distribution of those calls.

More information, along with the source code, can be found at http://sysprof.com/

# REFERENCES

+   - Free Software Foundation, 2014, 09a. GCC(1) Manual Page.
- Free Software Foundation, 2014, 09b. GCOV(1) Manual Page.
- Osier, J., Fenason, J., 1992. GNU gprof.
- Sandmann, S., 2013. Sysprof Source Repository. https://git.gnome.org/browse/sysprof/
- van de Ven, A., 2008.01. latencyop.c. $[LINUX_SRC]/kernel/latencyop.c. Linux Kernel Source File.
- van de Ven, A., 2009, 10. latencyop.c. Latencyop user space tool source.
- van de Ven, A. 2014. Powoport Source Repository. https://github.com/fenrus75/powoport