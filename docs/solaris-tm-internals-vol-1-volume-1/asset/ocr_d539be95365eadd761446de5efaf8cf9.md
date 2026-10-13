of the machine-specific page structure are hidden from the generic kernel—only the HAT machine-specific layer can see or manipulate its contents. Figure 5.19 shows how each page structure is embedded in a machine-dependent struct
machpage.

![](bbox=[0.237, 0.202, 0.805, 0.569])

**Figure 5.19** *Machine-Specific Page Structures: sun4u Example*

The machine-specific page contains a pointer to the HAT-specific mapping information, and information about the page’s HAT state is stored in the machine-specific machpage. The store information includes bits that indicate whether the page has been referenced or modified, for use in the page scanner (covered later in the chapter). Both the machine-independent and machine-dependent page structures share the same start address in memory, so a pointer to a page structure can be cast to a pointer to a machine-specific page structure (see Figure 5.19). Macros for converting between machine-independent pages and machine-dependent page structures make the cast.

# 5.7.4 Physical Page Lists

The Solaris kernel uses a segmented global physical page list, consisting of segments of contiguous physical memory. (Many hardware platforms now present memory in noncontiguous groups.) Contiguous physical memory segments are added during system boot. They are also added and deleted dynamically when