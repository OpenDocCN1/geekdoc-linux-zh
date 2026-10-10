![](bbox=[0.26, 0.08, 0.71, 0.36])

**Figure 7.6**
Prototypoe cape with potentiometer.

# ## Accessing the Analog Subsystem

The analog subsystem is fairly complex, and we won’t try to access it directly from user space. Instead we will use the `/sys` file system, similar to what we did earlier to turn off the LED triggers. The Resources section references a couple of pages with “recipes”, if you will, for setting up the `/sys` files to read the ADC. This completely nonintuitive procedure is embodied in the script file `samples/src/adc_on.sh`. The first line essentially installs the ADC subsystem and creates a set of files under `/sys/devices/ocp.x/helper.x`, named `AIN0` to `AIN7`. The second line shows you where these files actually are. Once you have determined the values for `x` and `y`, you can eliminate the second line. They will not change.

To read an analog input, you just open the corresponding `AIN` file and read it. These files return the value in millivolts, so the range is 0 to about 1800. There is a second set of files in `/sys/devices/ocp.x/44e0d000.tscadc/tiadc/io:device0` called `in_voltage0_raw` to `in_voltage7_raw` that return the raw 12-bit value.

Good programming practice dictates that there be a clear separation between code that is hardware independent, and code that actually manipulates `I/O` registers. At the very least, hardware-dependent code should be in a separate module from the purely application code. In the LED example, we “cheated” somewhat, in that the hardware-dependent code was mixed in with the main program in a single source file. In that case it did not matter much, because the objective was to illustrate how hardware access works without introducing any kind of application.