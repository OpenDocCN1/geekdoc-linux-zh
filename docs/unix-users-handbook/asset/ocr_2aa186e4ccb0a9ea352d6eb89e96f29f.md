chapter for HP-UX. You can see, however, that the outputs are very similar.

Processes are classified into one of three categories: runnable (“r”), blocked on I/O or short-term resources (“b”), or swapped (“w”).

Next you will see information about memory. “avm” is the number of virtual memory pages owned by processes that have run within the last 20 seconds. If this number is roughly the size of physical memory minus your kernel, then you are near paging. The “free” column indicates the number of pages on the system’s free list. It doesn’t mean that the process is finished running and these pages won’t be accessed again; it just means that they have not been accessed recently. I suggest that you ignore this column.

Next is paging activity. The first field (“re”) is particularly useful. It shows the pages that were reclaimed. These pages made it to the free list but were later referenced and had to be salvaged. Check to see that “re” is a low number. If you are reclaiming pages that were thought to be free by the system, then you are wasting valuable time salvaging these. Reclaiming pages is also a symptom that you are short on memory.

Next you see the number of faults in three categories: interrupts per second, which usually come from hardware (“in”), system calls per second (“sy”), and context switches per second (“cs”).

The final output is CPU usage percentage for user (“us”), system (“sy”), and idle (“id”). This is not as complete as the **iostat** output, which also shows **nice** entries.

You want to verify that the runnable processes (“r”) value is higher than the blocked (“b”) value and the runnable but swapped (“w”) processes value. If too many processes are blocked and swapped, your users will get a slower response time.

Whenever you see entries in the blocked (“b”) or runnable-but-swapped (“w”) columns, you see evidence that processes are standing still. You want to identify the source of the blocked and runnable-but-swapped processes. The reason will usually be insufficient RAM in your system. Swapped processes are those that have been moved from RAM to disk in an effort to free up RAM for other processes.

The following output shows a system in which there are many swapped processes occur:

![](bbox=[0.86, 0.58, 0.97, 0.68])