Figure 19.5 illustrates the relationship between the various hardware and software components in a SANE-driven scanning system. SANE’s mediation means that you can change a scanner (and hence a SANE driver) at will, and continue to use your scanning software just as you had before the change.

![](bbox=[0.25, 0.24, 0.8, 0.66])

# FIGURE 19.5

> SANE presents a uniform face to applications that can use a scanner.

Because SANE is the component that most directly communicates with the scanner, it’s here that you need to look for drivers. The SANE project includes support for most SCSI scanners, a handful of parallel-port scanners, and a growing number of USB scanners. You can find SANE drivers for some devices from third parties, but tracking them down can be difficult. In fact, your efforts might be in vain. In general, it’s best to use a device whose drivers come with SANE.