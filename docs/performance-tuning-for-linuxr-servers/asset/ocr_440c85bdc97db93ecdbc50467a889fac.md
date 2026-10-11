mainframe technology circa 2000, see http://www.research.ibm.com/journal/rd43-56.html.

These machines are optimal for server consolidation. They can support hundreds to thousands of discrete Linux images. Workload types suited to run in this environment exhibit the following characteristics:

+   I/O-intensive operations (for example, serving web pages)

+   Lightly loaded servers

Computation-intensive, graphic-oriented workloads are not good matches for mainframe serversnor are workloads that check the system clock often. Heavily loaded servers also are not good candidates for consolidation on a mainframe server.

Older mainframe did not support IEEE-format floating-point operations. Thus, all floating-point operations under Linux had to be converted to the IBM proprietary format, executed, and then converted back to IEEE format. Newer mainframes support IEEE format and do not pay this performance penalty.

Advanced mainframe system management and programming skills are needed for planning and installing a Linux deployment under z/VM. However, after the system is installed and configured, adding new virtual servers is fairly simple.

# ## Hardware Design Overview

The IBM zSeries architecture implements either 12 or 20 processors on a processor module. There are multiple types of processors, which are determined by the microcode that is loaded that controls the processor. The principal types of processors are the processor units, which are equivalent to CPUs on most servers, and the System Assist Processor (SAP), which handles control of the I/O operations. Each machine has at least two SAPs, and could have more depending on the I/O capacity needs.

The modules have two large L2 caches, with each L2 cache shared among half the processors on the module. This differs from stándard servers that have an L2 cache associated with each processor. The shared L2 cache allows a process to migrate between processors without losing its cache warmth.

Memory bandwidth is 1.5GBps per processor with an aggregate system bandwidth of 24GBps. The very large memory bandwidth design favors applications that do not have cache-friendly working sets or behavior.

Normal Linux servers usually run at no more than 50% average utilization to provide headroom for workload spikes. The design of the mainframes allows systems to run at 80% to 90% utilization.

# ### Reliability