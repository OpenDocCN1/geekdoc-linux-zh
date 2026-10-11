# FIGURE 15.9

The output of various proc commands

![](bbox=[0.27, 0.11, 0.88, 0.57])

+   **psig** Use the `psig` <PIDnumber> command to display process signal actions.
+   
+   **pstack** The `pstack` <PIDnumber> command performs a stack trace (similar to an LWP) and outputs the results in hexadecimal form.
+   
+   **ptree** The `ptree` <PIDnumber> command outputs the hierarchical tree representation of a process and its subprocesses. Figure 15.9 shows an example. Again, the `ptree` command is very useful for exposing operational dependencies.
+   
+   **pwait** Use the `pwait` command to display the status of a process after it terminates.
+   
+   **pwdx** Use the `pwdx` <PIDnumber> command to display a process's current working directory.