# Intel® VTune™ Amplifier XE 7

# CHAPTER CONTENTS

+   7.1 Installation and Configuration ................................................................ 120
    7.1.1 Building the Kernel Modules ................................................................ 121
    7.1.2 System Configuration ....................................................................... 122
7.2 Data Collection and Reporting ................................................................ 124
    7.2.1 Collect Action ....................................................................................... 125
    Configuration. ................................................................................................... 127
    7.2.2 Finalize Action ...................................................................................... 129
7.2.3 Report Action ....................................................................................... 129
    Command-Line Interface .................................................................................... 129
    Graphical Interface ................................................................................................ 131
References ................................................................................................................... 135

Intel® VTune™ Amplifier XE is a powerful cross-platform profiler capable of performing algorithm analysis, PMU sampling, and power analysis. The tool is comprised of a few components, including a set of Linux kernel drivers, which are responsible for performing the data collection, as well as command-line and GUI tools for controlling the drivers and generating reports.

By default, VTune installs a significant amount of documentation into ${VTINSTALL}/documentation. This includes walkthroughs and guides for collecting data and analyzing the result. Additionally, the documentation also provides a series of reference documents, including a reference of event metrics and their meanings, as well as a copy of the second volume of the Intel® Software Developer Manual, listing all of the instructions and their encodings.

Once installed, updates to VTune are conducted through the Intel® Software Manager, which is typically installed to /opt/intel/ism. Through this Java application it is possible to download and install updates to all Intel software products as they are released. Typically, VTune releases are grouped into optional and recommended updates. Optional updates occur more frequently and provide earlier access to new features. On the other hand, recommended updates occur less frequently, and combine all of the previous optional updates. As a result, the