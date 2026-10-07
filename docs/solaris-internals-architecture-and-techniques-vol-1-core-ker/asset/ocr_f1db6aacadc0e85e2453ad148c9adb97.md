# Table 5-13 Page Scanner Parameters (Continued)

| Parameter | Description | Min | 2.7 Default |
|---|---|---|---|n| minfree | If free memory falls below minify, then the page scanner is signaled to start every time a new page is created. | | desfree/2 |
| throttlefree | The number at which the page_create routines make the caller wait until free pages are available. | | minfree |
| fastscan | The rate of pages scanned per second when free memory = minfree. Measured in pages. | slow-scan | Minimum of 64 MB/s or 1/2 memory size |
| slowscan | The rate of pages scanned per second when free memory = lotsfree. | | 100 |
| maxpgio | A throttle for the maximum number of pages per second that swap device can handle. | ~60 | 60 or 90 pages/s |
| hand-spreadpages | The number of pages between the front hand clearing the reference bit and the back hand checking the reference bit. | 1 | fastscan |

#  5.8.5 Page Scanner Implementation

The page scanner is implemented as two kernel threads, both of which process number 2, "pageout". One thread scans pages, and the other thread pushes the dirty pages queued for I/O to the swap device. In addition, the kernel callout mechanism wakes the page scanner thread when memory is insufficient. (The kernel callout scheduling mechanism is discussed in detail in Section 2.5, "The Kernel Callout Table," on page 47.)

The scanner scheduling() function is called four times per second by a callout placed in the callout table. The scheduling() function checks whether free memory is below the threshold (lotsfree or cachefree) and, if required, triggers the scanner thread. The page scanner is not only awakened by the callout thread, it is also triggered by the page allocator if memory falls below throttle-free.