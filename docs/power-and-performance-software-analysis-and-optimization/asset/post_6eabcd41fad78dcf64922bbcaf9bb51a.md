
## 7.2 Data collection and reporting

On the other hand, the command-line interface does not use the project files created by the GUI, nor does it create its own. Instead, each configuration option must be specified as a command-line argument. The author assumes this is because the command-line interface yields itself well to scripting, so any functionality provided by a project file can be replicated, with less effort, through the creation of a shell script.

The comprehensive list of available configuration options and their meanings can be found in the VTune documentation, the pages for each command, or through the help command built into the command-line tool. For example, executing `amplify-cl` will list the available actions, executing `amplify-cl-help` will list all of the possible configuration options for that specific action.

At the time of this writing, there are eight actions available in the command line interface. For profiling situations, knowledge of only two of these is necessary. These include the collect action, which performs the actual data collection, and the report action, which summarizes the data collected during the collect action in a human readable format.

### 7.2.1 COLLECT ACTION

The data is determined by the specified analysis type. To simplify data collection, VTune combines the building blocks of data collection into a high-level structure known as an analysis type. An analysis type is comprised of one or more data points, PMU events although other metrics are supported, with "knobs" for controlling the behavior of the data collection. Through the use of analysis types, VTune simplifies the process of creating, running, and sharing complicated performance analyses.

VTune provides a predefined of analysis types designed by Intel engineers to cover the most common profiling situations. Additionally, the user is free to create their own analysis types. Each analysis type is defined in an XML file. The predefined types are located at `$VTUNE_INSTALL/config/analysis_type`, while the user's custom types are defined in `$HOME/intel/amplxe/analysis_type`. Each analysis is categorized as either algorithmic analysis or a microarchitectural analysis. In general, the algorithmic analyses are available for most x86 processors, while the microarchitectural analyses depend on features present in some PMUs. As a result, the microarchitectural analyses are further divided into Intel SKUs within a hardware generation support all of the PMU features required for every analysis within that generation's category. When performing microarchitectural analysis, the general-exploration analysis type is a good starting point, since it is designed to automatically perform the Top-Down profiling methodology described in Section 6.2.

The analysis type is a required argument for the command-line interface and should immediately follow the -collect argument. The last argument provided should be the command to profile. For instance, if the bandwidth analysis type was desired to run on the executable `foo`, the command invocation, without any further configurations, would be `amplify-cl collect bandwidth foo`. Additionally, VTune is capable of attaching to an existing process. In lieu of providing the command to execute, the -target-pid or -target-process arguments specify the pid or name of the existing process to attach to.

Once the collection has completed, a results directory will be comprised of three separate components. The first component is the lower case letter “r”. The second component is a three-digit number, representing the analysis type. Finally, the third component is an abbreviation of the analysis type. Continuing the previous example with the knowledge that bandwidth analysis is abbreviated as `bw`, the first run would produce a directory `r000bw`, the second run would produce a directory `r001bw`, and so on.

In the graphical interface, data collection begins by right-clicking the name in the Project Navigator window and selecting the New Analysis menu item, or by clicking the menubar shortcut that resembles an orange triangle to the right. This will open a hierarchical list of the available analysis types and their subsequent configuration options. Figure 7.2 illustrates this.

Notice that in the bottom right side of the window is a button labeled Command Line. Selecting this button will display the exact `amplify-cl` command that will be executed. This will show you how the GUI is performing some actions.

![](img/33fad1fa149d4f0cdd55ff2565970ab2_143_0.png)

FIGURE 7.2

Intel® VTune™ Amplifier GUI analysis type selection.

## Configuration

Between the -collect argument and the final argument, the application to profile, are the configuration options that control how the analysis occurs and is interpreted. In the graphical interface, all of these configuration items are set within the project properties.

Typically, the user wants to correlate data samples from addresses to lines of source code. In order for this to work properly, the user needs to specify where the source and binary files are located. The -source-search-dir= argument adds -search-dir argument to the binary search path. Both of these arguments may be duplicated as many times as necessary.

As discussed in Chapter 6, the PMU can only monitor a limited number of events simultaneously. As a result, there are a number of techniques for handling the situation where more events are specified than collected can be enabled simultaneously. In this situation, the set of events is partitioned into subsets capable of being programmed together. If the program can execute only once, as is the case with the default VTune collection, these subsets take being enabled on the PMU. The -multiple-runs argument allows for the data collection to run multiple times, each time with a different subset of the events active. As a result, this option minimizes the error of multiplexing the events. Obviously for this to work correctly, the executable must be capable of executing repeatedly without user interaction between runs.

When profiling with sampling, it is necessary to determine an appropriate sampling frequency, that how frequently the PMU events should be collected. Some analysis types support a configuration option, referred to as a knob, that controls the sampling interval. This knob, sampling-interval, specifies the number of milliseconds between collections, ranging from 1 to 1000 ms. The default interval is 10 ms. Not all analysis types support the analysis type, which can be configured via a -knob interval=value command-line argument. For example, in order to increase the interval to 100 ms for an advanced-hotspots analysis type, the command would look like `amplify -c collect advanced-hotspots -knob sampling-interval=100`.

In order to simplify the collection of the sampling interval, VTune also exposes a -target-type=category command-line argument. This argument is supported for all analysis types, whether they support the sampling interval. Rather than specifying an exact interval, the user categorizes the estimated duration of the application's execution. Based on this, VTune automatically configures the collection intervals. There are four duration categories. The first category, veryhort, specifies that the program execution is. The second category, short, specifies that the program execution is. The third category, medium, specifies that the program execution is. The fourth category, long, specifies that the program execution

The -call-stack-mode argument filters functions should appear in the trace. There are three valid values for mode:
- user-only: only records functions present within the profiled execution. As a result, kernel functions do not appear in the trace. This is the default mode.
- user-plus: records all of the functions that would be recorded in user-only mode, but also kernel functions directly invoked by the application. As a result, the internal kernel stack filters out any the internal kernel call chains.
- all: records all functions, both within the application and the kernel.

Additionally, inline functions can be included within the call stack via the -inline-mode-on, or excluded via -inline-mode-off, command line argument.

By default, all data collection is performed on the local system; however, VTune supports data collection over the SSH and ADB (Android Debug Bridge) protocols. For this type of writing, the ADB protocol is only supported in the version of VTune provided with Intel® System Studio. With remote data collection, the collect action will be specified on the host system, and then the results will be copied back to the host system for local analysis.

In remote data collection to work, the data collection kernel modules that described in Section 7.1 must be installed and enabled on the remote system. When profiling a remote embedded device, the collect drivers on the host system, and add them to the system image that will be provisioned on the device. Additionally, in order to fit within size constraints, it is possible to skip the installation of the graphical interface tools and libraries. Within the VTune tarball, there is a directory named CLI_Install. This directory contains the scripts and files required for a manual installation, consisting of only the command-line tools and data collection drivers. These files can either be installed directly into the system image for the remote device before provisioning, or physically copied onto the remote device and installed manually.

Once the remote system is configured for data collection, and for the remote protocol, data collection can begin on the host system by specifying the protocol,
