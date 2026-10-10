Let us set a breakpoint at line 34 in sort_utils.c. That is the beginning of an if statement in read_file(). Right-click in the marker bar at line 34, and select Toggle Breakpoint. A green circle appears to indicate that an enabled breakpoint is set at this location. The check mark indicates that the breakpoint was successfully installed.

A new entry appears in the Breakpoints view, with the full path to the breakpoint. The check box shows that the breakpoint is enabled. Click on the check box to disable the breakpoint, and note that the circle in the marker bar changes to white. Disabled breakpoints are ignored by the debugger. Click the check box again to re-enable it.

Click Resume in the Debug view tool bar, and the program proceeds to the breakpoint. The Thread [0] entry in the Debug view indicates that the thread is suspended, because it hit a breakpoint. Click Step Over to load temp with the first record. Select the Variables view and click the white arrow next to temp. Now you can see the current values of the fields in temp. Variables whose value has changed since the last time the thread was suspended are highlighted in yellow.

Breakpoints have some interesting properties that we will explore later on.

# ## Memory View

There is one more debug-oriented view that shows up by default in the bottom tabbed window of the Debug perspective. The Memory view lets you monitor and modify process memory. Memory is organized as a list of memory monitors, where each monitor represents a section of memory specified by a base address. Each memory monitor can be displayed in one or more of four predefined formats known as memory renderings. The predefined renderings are hexadecimal (default), ASCII, signed integer, and unsigned integer.

Fig. 5.9 shows a memory monitor of the area allocated for temp just after the first fscanf( ) call in read_file(). The Memory view is split into two panes, one that lists the currently active monitors and another that displays the renderings for the selected

![](bbox=[0.13, 0.79, 0.88, 0.88])

Memory view.