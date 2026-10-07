Section "Monitor"

```
Identifier "Generic Monitor"
VendorName "Unknown"
ModelName "Unknown"
```

The entries in this section are text strings only and have no real configuration value for XFree86. The only time they are used is when the text strings are echoed back to you when XFree86 starts up or a utility displays configuration information. You can enter the proper values for these items to make XFree86 a little more friendly to work with.

The next subsection deals with the horizontal bandwidth of the monitor. This is an important section, and you should try to find the actual values for your monitor. Some settings for specific brands are listed in the documentation accompanying XFree86, especially in the documents Monitors and VideoModes.doc. Check your distribution directories for any specification document files. If you can't find specific values for these settings, use the lowest setting as a default, unless you know your monitor is capable of higher values. The bandwidth section looks like this:

```
# Bandwidth is in MHz unless units are specified

Bandwidth 25.2
```

```
# HorizSync is in KHz unless units are specified.
# HorizSync may be a comma separated list of discrete values, or a
# comma separated list of ranges of values.
# NOTE: THE VALUES HERE ARE EXAMPLES ONLY. REFER TO YOUR MONITOR'S
# USER MANUAL FOR THE CORRECT NUMBERS.

HorizSync 31.5 # typical for a single frequency fixed-sync monitor

# HorizSync 30-64 # multisync
# HorizSync 31.5, 35.2 # multiple fixed sync frequencies
# HorizSync 15-25, 30-50 # multiple ranges of sync frequencies
```

The bandwidth settings have good comments next to them, as shown in the preceding code. If you were installing a multisync monitor, for example, you could comment out the 31.5K Hz line and uncomment the 30-64 KHz line.

The vertical refresh rate is set in another subsection and is as critical to your monitor's good health as the bandwidth. Again, check the documentation for more information. The vertical refresh subsection code looks like this:

```
# VertRefresh is in Hz unless units are specified.
# VertRefresh may be a comma separated list of discrete values, or a
# comma separated list of ranges of values.
# NOTE: THE VALUES HERE ARE EXAMPLES ONLY. REFER TO YOUR MONITOR'S
# USER MANUAL FOR THE CORRECT NUMBERS.
```