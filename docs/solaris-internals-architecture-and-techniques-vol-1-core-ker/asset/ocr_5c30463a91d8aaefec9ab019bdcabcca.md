![](bbox=[0.09852, 0.0935, 0.85675, 0.4635])

Figure 5.23 Page Scanner Rate, Interpolated by Number of Free Pages

Figure 5.23 shows the rate at which the scanner scans increases linearly as free memory ranges between between lotsfree and zero. The scanner starts scanning at the minimum rate set by slowscan when memory falls below lotsfree and then increases to fastscan if memory falls low enough.

The number of pages scanned increases from the slowest rate (set by slowscan when lotsfree pages are free) to a maximum determined by the system parameter fastscan. Free memory never actually reaches zero, but for simplicity the algorithm calculates the maximum interpolated interpolate rate against the free memory ranging between lotsfree and zero. In our example system with 1 Gbyte of physical memory (shown in Figure 5.24 on page 185), we can see that the scanner starts scanning when free memory falls to 16 Mbytes plus the short-term memory deficit.