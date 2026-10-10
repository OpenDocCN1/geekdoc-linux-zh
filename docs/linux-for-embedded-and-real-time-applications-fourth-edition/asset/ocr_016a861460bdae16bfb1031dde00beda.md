![](bbox=[0.12, 0.07, 0.88, 0.53])

advances to the next line, and *sort* in the Variable view shows its initial value of 1. The value is highlighted in yellow, because it has changed since the last time the debugger was suspended. You can also see the current value of any variable by simply rolling the cursor over it. Give it a try.

For now, go ahead and let the program run by clicking the Resume icon in the main tool bar. Hmmmm, we didn't get exactly the results we expected. *datafile* has 12 records, but only 1 record is output to the Console view. That is because a couple of run-time errors have been built into the program to offer some practice using the debugger.

# The Debug View

In the Debug view, right-click on the top level project entry and select *Relaunch* to start another debug run. The Debug view, shown in *Fig. 5.8*, displays the state of the program in a hierarchal form. At the top of the hierarchy is a *launch instance*, that is an instance of a launch configuration identified by its name. Below that is the debugger instance, identified by the name of the debugger, in this case *gdb*. Beneath the debugger are the program threads under the debugger's control. For *record_sort* there is just one thread. Later on we will see how gdb/Eclipse handles multithreaded programs.