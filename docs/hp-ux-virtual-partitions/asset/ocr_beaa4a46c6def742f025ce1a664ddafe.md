manages the physical console. This ensures that the physical console will be available even if the vPar that owns it is not running.

We can also use SAM to view all aspects of the kernel and make changes to the kernel for vPars. Keep in mind that running SAM in different vPars is like running SAM on different systems. Figure 4-2 shows a screen shot of SAM displaying drivers for vPar `cable1` (hostname of `cvhdc0n4`) shown in the top of all of the SAM windows):

![](bbox=[0.12, 0.29, 0.84, 0.77])

Note in the lower left window of Figure 4-2 that `vcn`, `vcs`, and `vpar_driver` have a *Current State* of *In*, indicating that the kernel has these three drivers present in it.