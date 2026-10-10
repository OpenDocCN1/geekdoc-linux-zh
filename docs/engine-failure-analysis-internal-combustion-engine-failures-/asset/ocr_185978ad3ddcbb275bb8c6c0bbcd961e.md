*(filename2)*. It can merge differences in one of the newer files to the other newer file. If all three files differ in the same place, the instance is called *overlapping*.

See also *cmp*, *comm*, *diff*.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| **-3** | Create an **ed** script that incorporates all changes between *filename2* (the original file) and *filename3* into the *filename1*, but make changes only when they are non-overlapping |
| **-A**, **--show-all** | Incorporate all changes, surrounding all conflicts with bracket lines |
| **-a**, **--text** | Treat all files as text and compare them line by line |
| **-e**, **--ed** | Create an **ed** script that incorporates all changes between *filename2* (the original file) and *filename3* into *filename1* |
| **-E**, **--show-overlap** | Create an **ed** script that incorporates all changes between *filename2* (the original file) and *filename3* into *filename1* and show the overlap conflicts in brackets |
| **-m**, **--merge** | Directly incorporate all changes between *filename2* (the original file) and *filename3* into *filename1*, without making an **ed** script |
| **-T**, **--initial-tab** | Display with a tab before each line |
| **-v**, **--version** | Show the version number |
| **-X** | Create an **ed** script to incorporate all overlap conflicts into *filename1* and show the overlap conflicts with brackets |
| **-x**, **--overlap-only** | Create an **ed** script to incorporate all overlap conflicts into *filename1* |