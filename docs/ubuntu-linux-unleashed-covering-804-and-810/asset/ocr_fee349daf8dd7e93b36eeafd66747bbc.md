# 11  Automating Tasks

+   Running Services at Bootup ................................................................................................234
+   Beginning the Boot Loading Process ....................................................................................234
+   &nbsp;&nbsp;&nbsp;&nbsp;Loading the Linux Kernel ...............................................................................................235
+   &nbsp;&nbsp;&nbsp;&nbsp;System Services and Runlevels .......................................................................................236
+   &nbsp;&nbsp;&nbsp;&nbsp;Runlevel Definitions ........................................................................................................236
+   &nbsp;&nbsp;&nbsp;&nbsp;Booting into the Default Runlevel .....................................................................................237
+   &nbsp;&nbsp;&nbsp;&nbsp;Booting to a Non-Default Runlevel with GRUB .................................................................237
+   &nbsp;&nbsp;&nbsp;&nbsp;Understanding init Scripts and the Final Stage of Initialization ..........................................238
+   &nbsp;&nbsp;&nbsp;&nbsp;Controlling Services at Boot with Administrative Tools .....................................................239
+   &nbsp;&nbsp;&nbsp;&nbsp;Changing Runlevels ..........................................................................................................240
+   &nbsp;&nbsp;&nbsp;&nbsp;Troubleshooting Runlevel Problems ..................................................................................240
+   Starting and Stopping Services Manually ..............................................................................241
+   Scheduling Tasks ....................................................................................................................242
+   &nbsp;&nbsp;&nbsp;&nbsp;Using at and batch to Schedule Tasks for Later .................................................................242
+   &nbsp;&nbsp;&nbsp;&nbsp;Using cron to Run Jobs Repeatedly ...................................................................................245
+   Basic Shell Control ..................................................................................................................248
+   &nbsp;&nbsp;&nbsp;&nbsp;The Shell Command Line ..................................................................................................248
+   &nbsp;&nbsp;&nbsp;&nbsp;Shell Pattern-Matching Support ........................................................................................250
+   &nbsp;&nbsp;&nbsp;&nbsp;Redirecting Input and Output ............................................................................................251
+   &nbsp;&nbsp;&nbsp;&nbsp;Piping Data .......................................................................................................................252
+   &nbsp;&nbsp;&nbsp;&nbsp;Background Processing .....................................................................................................252
+   Writing and Executing a Shell Script ......................................................................................253
+   &nbsp;&nbsp;&nbsp;&nbsp;Running the New Shell Program .......................................................................................254
+   &nbsp;&nbsp;&nbsp;&nbsp;Storing Shell Scripts for Systemwide Access ....................................................................255
+   &nbsp;&nbsp;&nbsp;&nbsp;Interpreting Shell Scripts through Specific Shells ..............................................................256
+   &nbsp;&nbsp;&nbsp;&nbsp;Using Variables in Shell Scripts ........................................................................................258
+   &nbsp;&nbsp;&nbsp;&nbsp;Assigning a Value to a Variable ........................................................................................258
+   &nbsp;&nbsp;&nbsp;&nbsp;Accessing Variable Values ................................................................................................259
+   &nbsp;&nbsp;&nbsp;&nbsp;Positional Parameters ........................................................................................................259
+   &nbsp;&nbsp;&nbsp;&nbsp;A Simple Example of a Positional Parameter ....................................................................259
+   &nbsp;&nbsp;&nbsp;&nbsp;Using Positional Parameters to Access and Retrieve
+   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Variables from the Command Line ................................................................................260
+   &nbsp;&nbsp;&nbsp;&nbsp;Using a Simple Script to Automate Tasks ..........................................................................261
+   &nbsp;&nbsp;&nbsp;&nbsp;Built-In Variables ...............................................................................................................263
+   &nbsp;&nbsp;&nbsp;&nbsp;Special Characters .............................................................................................................263
+   &nbsp;&nbsp;&nbsp;&nbsp;Use Double Quotes to Resolve Variables in Strings with
+   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Embedded Spaces ............................................................................................................264
+   &nbsp;&nbsp;&nbsp;&nbsp;Using Single Quotes to Maintain Unexpanded Variables ....................................................265
+   &nbsp;&nbsp;&nbsp;&nbsp;Using the Backslash as an Escape Character ......................................................................266
+   &nbsp;&nbsp;&nbsp;&nbsp;Using the Backtick to Replace a String with Output ..........................................................266
+   &nbsp;&nbsp;&nbsp;&nbsp;Comparison of Expressions in pdksh and bash ..................................................................267