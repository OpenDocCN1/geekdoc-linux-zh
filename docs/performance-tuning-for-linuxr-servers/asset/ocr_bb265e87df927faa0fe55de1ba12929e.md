# System (Registered) Monitors

| %MISS | GETS | NONREC | SLOW | REC | TIER2 | TIER3 | %UTIL | AVER-HTM | MON-NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 87 | 5273 | 5273 | 4572 | 0 | 710708 | 18487 | 1 | 95408 | ITC Global Compile lock |
| 9 | 6870 | 6869 | 631 | 1 | 113420 | 2976 | 0 | 11807 | Heap lock |
| 5 | 1123 | 1123 | 51 | 0 | 11098 | 286 | 1 | 248385 | BinClass lock |
| 0 | 1153 | 1147 | 5 | 6 | 1307 | 33 | 0 | 47974 | Monitor Cache lock |
| 0 | 46149 | 45877 | 134 | 272 | 34961 | 877 | 1 | 6558 | ITC CSA lock |
| 0 | 33734 | 23483 | 19 | 10251 | 6544 | 150 | 1 | 17083 | Thread queue lock |
| 0 | 5 | 5 | 0 | 0 | 0 | 0 | 0 | 9309689 | JNI Global Reference lock |
| 0 | 5 | 5 | 0 | 0 | 0 | 0 | 0 | 9283000 | JNI Pinning lock |
| 0 | 5 | 5 | 0 | 0 | 0 | 0 | 0 | 9442968 | Sleep lock |
| 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | Monitor Registry lock |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | Evacuation Region lock |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | Method trace lock |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | ClassLoader lock |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | Heap Promotion lock |

# Java (Inflated) Monitors

| %MISS | GETS | NONREC | SLOW | REC | TIER2 | TIER3 | %UTIL | AVER-HTM | MON-NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 15 | 68 | 68 | 10 | 0 | 2204 | 56 | 2 | 11936405 | test.lock.testlock1@A09410 |
| ▶ A09418 | 2 | 42 | 42 | 1 | 0 | 186 | 5 | 0 | 300478 | test.lock.testlock2@D31358 |
| ▶/D31360 | 0 | 70 | 70 | 0 | 0 | 41 | 1 | 0 | 7617 | java.lang.ref.ReferenceQueue$Lock@920628/920630 |

LEGEND:

MISS : 100 * SLOW / NONREC
GETS : Lock Entries
NONREC : Non Recursive Gets
SLOW : Non Recursions that Wait
REC : Recursive Gets
TIER2 : SMP Wait Hierarchy
TIER3 : SMP Wait Hierarchy
%UTIL : 100 * Hold-Time / Total-Time
AVER-HTM : Hold-Time / NONREC

Descriptions of the report's fields are as follows:

+   • JIT_Interval_Time. Time interval between the start and end of measurement. Time is expressed in the units appropriate for the hardware platform: cycles for x86, IA64, and S390, and time-based ticks for PPC.

+   • MISS. Percentage of the total GETS (acquires) where the requesting thread was blocked waiting on the monitor.
+   
+   MISS = (SLOW / NONREC) * 100

+   • GETS. Total number of successful acquires.
+   
+   GETS = FAST + SLOW + REC

+   • NONREC. Total number of nonrecursive acquires. This number includes SLOW gets.

+   • SLOW. Total number of nonrecursive acquires which caused the requesting thread to block waiting for the monitor to no longer be owned. This number is included in NONREC.
+   
+   To calculate the number of nonrecursive acquires in which the requesting thread obtained ownership immediately (FAST), subtract SLOW from NONREC. On platforms that support 3-Tier Spin Locking, monitors