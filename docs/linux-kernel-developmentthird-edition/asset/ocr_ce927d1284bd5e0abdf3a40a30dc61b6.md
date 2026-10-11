viii Contents

# 3 Process Management 23

+   The Process 23
+   Process Descriptor and the Task Structure 24
+   Allocating the Process Descriptor 25
+   Storing the Process Descriptor 26
+   Process State 27
+   Manipulating the Current Process State 29
+   Process Context 29
+   The Process Family Tree 29
+   Process Creation 31
+   Copy-on-Write 31
+   Forking 32
+   vfork() 33
+   The Linux Implementation of Threads 33
+   Creating Threads 34
+   Kernel Threads 35
+   Process Termination 36
+   Removing the Process Descriptor 37
+   The Dilemma of the Parentless Task 38
+   Conclusion 40

# 4 Process Scheduling 41

+   Multitasking 41
+   Linux's Process Scheduler 42
+   Policy 43
+   I/O-Bound Versus Processor-Bound Processes 43
+   Process Priority 44
+   Timeslice 45
+   The Scheduling Policy in Action 45
+   The Linux Scheduling Algorithm 46
+   Scheduler Classes 46
+   Process Scheduling in Unix Systems 47
+   Fair Scheduling 48
+   The Linux Scheduling Implementation 50
+   Time Accounting 50
+   The Scheduler Entity Structure 50
+   The Virtual Runtime 51