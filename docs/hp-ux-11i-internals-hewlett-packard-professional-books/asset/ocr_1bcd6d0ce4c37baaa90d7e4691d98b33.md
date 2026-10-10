# Contents

+   - System-Level and User-Level Priorities 132
+   - Time Basics in HP-UX Scheduling: The Tick 132
+   - Time Slicing or Round-Robin Queuing 133
+   - Priority Decay, N ice and User-Level Priorities 133
+   - SCHED_NOAGE 135
+   - SCHED_RTPRIO 135
+   - POSIX Real-Time Scheduler 137
+   - Sizing the POSIX Queues 137
+   - SCHED_FIFO 138
+   - SCHED_RR 138
+   - SCHED_RR2 138
+   - Run Queues 138
+     - The Systemwide POSIX Run Queues 139
+     - Per-Processor Run Queues 141
+   - Summary 142

# Chapter 6 Managing Memory 143

+   - Types of Memory 144
+     - Logical Memory 144
+     - Virtual Memory 144
+     - Physical Memory 145
+     - Front Store and Back Store 145
+   - The System’s Virtual Address Space 146
+   - Virtual-to-Physical Page Tables 147
+   - The Kernel View: The Hash Table 152
+     - Page Frame to Virtual Page Frame Tables 154
+     - Virtual Address Aliasing 156
+     - Regions of Pages 157
+   - Shared Objects 161
+     - Virtual Page Locator, VFD, and DBD 161
+   - The b-tree 163
+   - broot, bnodes, and chunks 164
+   - Page Lists 166
+   - Connecting the Kernel View to the Process View 167
+     - Managing Page Frames: Many Points of View 168
+   - Keeping Track of Free Physical Page Frames 169
+   - Is a Page I/O Really Needed? (f hash and fhead) 172
+   - Views, Ponds, Pools, Pages 173