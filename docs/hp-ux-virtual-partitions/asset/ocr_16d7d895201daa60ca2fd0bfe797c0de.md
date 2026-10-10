+   - Install the HP-UX 11i *Operating Environment*.
+   - Set system parameters at the time of first boot after loading HP-UX 11i with **set\_parms**.
+   - Download and install select patches on your system (at the time of this writing there are many patches required to support vPars.)
+   - Install vPars software.
+   - Configure vPars.
+   - Install additional software.

You would typically load software in the order shown above: Install the base *Operating Environment*; boot your system and use **set\_parms**; load patches; install vPars software; configure vPars; and then install and configure all other software. You may want to view Chapter 10, which covers Ignite-UX. Among the material covered is an Ignite-UX procedure to load vPars written by an HP lab expert on vPars. If you’re setting up many vPars systems, this procedure may save you some time.

Since there is extensive background on loading HP-UX 11i in the non-vPars-specific section of the chapter, let’s jump to loading vPars software in the next section.

# # Loading the Software Required for Virtual Partitions

We cover installing Virtual Partitions software in this section. I assume that you already have HP-UX 11i installed on your system or know how to do so. If you have not yet installed HP-UX 11i on your system, please jump ahead to the non-vPars-specific section, which covers installing HP-UX 11i. We also earlier covered selecting devices on which to base your vPars and install HP-UX 11i.

Keep in mind that HP-UX must be loaded for each Virtual Partition you wish to run. If, for instance, you want to run two Virtual Partitions, as we do in our examples in this book, HP-UX 11i will need to be loaded for both Virtual Partitions. The procedure covered for loading HP-UX 11i needs to be performed for every Virtual Partition you want to run. HP-UX 11i can