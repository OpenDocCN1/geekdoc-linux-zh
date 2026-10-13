![](bbox=[0.1778, 0.1416, 0.7952, 0.4979])

**Figure 5.14** *Physical Swap After a Page-out Occurs*

When we exhaust physical swap space, we simply ignore the `putpage()` request for a page, resulting in memory performance problems that are very hard to analyze. A failure does not occur when physical swap space fills; during reservation, we ensured that we had sufficient available virtual swap space, comprising both physical memory and physical swap space. In this case, the `swapfs_putpage()` simply leaves the page in memory and does not push a page to physical swap. This means that once physical swap is 100 percent allocated, we begin effectively locking down the remaining pages in physical memory. For this reason, it’s often a bad idea to run with 100 percent physical swap allocation (`swap -l` shows 0 blocks free) because we might start locking down the wrong pages in memory and our working set might not correctly match the pages we really want in memory.

# 5.5.3 Anonymous Memory Accounting

The amount of anonymous memory in the system is recorded by the anon accounting structures. The anon layer keeps track of how anonymous pages are allocated