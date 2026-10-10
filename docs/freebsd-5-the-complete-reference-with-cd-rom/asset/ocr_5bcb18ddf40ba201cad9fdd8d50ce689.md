# top

In some respects, top is a variant of ps. Like ps, top lists running processes, but it does so in a dynamic way. By default, top sorts processes by CPU time. This makes top an extremely useful tool for spotting runaway processes—those that have locked themselves in infinite loops, consuming CPU time to no useful end. Figure 5-4 shows top in action.

Several top variants are available. For instance, the GNOME project ships with one called gtop, which provides a more GUI-oriented user interface. These GUI variants of top provide functionality similar to that in the standard text-based top, but users more comfortable with GUI tools may find them more intuitive. You can use a GUI top tool even from another environment; for instance, you can use gtop from KDE or when no desktop environment is running, although of course X must be running and you need supporting GNOME libraries.

![](bbox=[0.18, 0.42, 0.82, 0.82])

Figure 5-4. The top command updates its display to show changes in process demands on the system over time.