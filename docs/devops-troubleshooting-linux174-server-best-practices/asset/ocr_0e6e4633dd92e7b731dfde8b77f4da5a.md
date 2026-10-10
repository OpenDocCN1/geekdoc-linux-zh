![](bbox=[0.25, 0.05, 0.95, 0.32])

Figure 10-1 Memtest86+ testing some RAM

any errors, they will be reported in the results output at the bottom of the screen.

If you do find an error in your RAM, you may not automatically be able to identify which DIMM has the error. At this point, you will have to use the process of elimination to take out all but the minimal amount of RAM your system needs to boot (often a pair of DIMMs) and run Memtest86+ to see if that pair has an error. If the pair passes, put them in the good pile and continue on until you find a pair that has an error. Once you do, you can split the DIMM pair so you run Memtest86+ with one unknown DIMM and one known good DIMM until you can find which specific DIMM is bad. Of course, don’t be lazy, and be sure to test every DIMM before you put the server back together. I’ve seen circumstances where two different DIMMs in the same server had problems at the same time.

# ## Network Card Failures

When a network card starts to fail, it can be rather unnerving as you try all sorts of network troubleshooting steps to no real avail. Often when a