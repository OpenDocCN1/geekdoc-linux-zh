When free memory falls below `cache-free`, file pages (which are not mapped executable) are freed. The scanner starts scanning at a rate of `slowscan`.

When free memory falls below this threshold, the system starts freeing all writes and UFS read-ahead is disabled.

When free memory falls below `lots-free`, the scanner starts freeing anonymous (application heap) and executable pages in addition to file pages. This only happens when the scanner is not able to keep up with the rate of file system I/O.

If free memory falls to `desfree`, then NFS version 3 stops writing asynchronously, kernel async I/O stalls, and idle processes are swapped out.

When free memory falls below `cache-free`, pages that are not mapped executable are freed. The scanner starts scanning at a rate governed by `slowscan`.

Noncritical memory requests are blocked.

All memory requests are blocked.

The earth stops rotating if `freemem==0`.

![](bbox=[0.48, 0.13, 0.817, 0.812])

(Parameters are measured in units of pages.)

`cachefree`

`lotsfree + pages_before_pager`

`lotsfree`

`desfree`

`minfree`

`throttlefree`

(60) `pageout_reserve`

`0`

`slowscan`

The rate at which pages are made available to the file system varies with the scan rate and is capped by `fastscan` or 95% of 1 CPU.

`fastscan`

# **Figure 15.3** *VM Parameters That Affect File Systems*