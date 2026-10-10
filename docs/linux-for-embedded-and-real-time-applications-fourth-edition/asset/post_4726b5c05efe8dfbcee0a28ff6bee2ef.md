
![](img/f03d6fa2c5faefc793771df52bbb2ef9_126_0.png)

**Figure 7.6**
Prototyping cape with potentiometer.

## Accessing the Analog Subsystem

The analog subsystem is fairly complex, and we won’t try to access it directly from user space. Instead we will use the `/sys` file system, similar to what we did earlier to turn off the LED triggers. The Resources section references a couple of pages with “recipes”, if you will, for setting up the `/sys` files to read the ADC. This completely nonintuitive procedure is embodied in the script file `samples/src/adc_on.sh`. The first line essentially installs the ADC subsystem and creates a set of files under `/sys/devices/ocp.x/helper.x`, named `AIN0` to `AIN7`. The second line shows you where these files actually are. Once you have determined the values for `x` and `y`, you can eliminate the second line. They will not change.

To read an analog input, you just open the corresponding `AIN` file and read it. These files return the value in millivolts, so the range is 0 to about 1800. There is a second set of files in `/sys/devices/ocp.x/44e0d000.tscadc/tiadc/io:device0` called `in_voltage0_raw` to `in_voltage7_raw` that return the raw 12-bit value.

Good programming practice dictates that there be a clear separation between code that is hardware independent, and code that actually manipulates `I/O` registers. At the very least, hardware-dependent code should be in a separate module from the purely application code. In the LED example, we “cheated” somewhat, in that the hardware-dependent code was mixed in with the main program in a single source file. In that case it did not matter much, because the objective was to illustrate how hardware access works without introducing any kind of application.

In this example we will make a clear distinction between hardware-dependent code and the main program’s algorithm. Create a new Eclipse standard C Makefile project named `measure` located at `src/measure`. Open the source file `measure.c`. The first thing to notice is that once again we have those annoying “\?”” symbols next to the header files. But rather than laboriously retyping the paths to the headers, this time we will *export* some project settings from the `led` project, and *import* them into `measure`.

Proceed as follows:

- 1. Select the `led` project entry in the *Project Explorer* view. Right click and select *Properties*.
- 2. Expand `C/C++ General`, and select *Paths and Symbols*. Click the *Export Settings...* button.
- 3. Make sure the `led` project is selected, and uncheck *Symbols*.
- 4. Browse to `home/samples/src/`, and enter a file name. I used `includes`. The data will be saved as an XML file.
- 5. *Fig. 7.7* shows the final export dialog. Click Finish.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_127_0.png)

Figure 7.7
Export dialog.

Next are the steps for importing the project settings into the measure project:

- 1. Right-click the measure project entry in Project Explorer, and select Properties.
- 2. Expand C/C++ General and select Paths and Symbols. Click the Import Settings… button.
- 3. Browse to `home/samples/src/`, and select `includes.xml`. Click OK.
- 4. Click Finish.
- 5. Open the measure project properties, and verify that the include paths are present.

The program reads the A/D, and prints the value on stdout. It takes a command line argument that is the number of seconds between readings. The default is two.

This is a good time for me to make an observation about my sample programs. There is very little in the way of error or “sanity” checking in these examples. If you enter something incorrectly, chances are the program will crash. That is not much of a problem in this example, but can be a problem in later examples that require more extensive input.

I feel that adding a lot of error checking code gets in the way of communicating the point the example is trying to make. Feel free to add some error checking logic if you like.

Back in the program, the important point to note is that most of the details of dealing with the A/D converter and digital I/O are “hidden” behind APIs (Application Programming Interface) that present data in a form useful to the application. The application need not concern itself with the details of setting up the peripherals, it simply calls the appropriate “init” functions. Then it reads and writes data until the user terminates the program. Finally, it “closes” the peripheral devices.

The file `trgrdive.c` implements the “device driver” APIs. The reason for naming it “trgrdive” will become apparent in the next chapter. There are two peripheral initialization functions: `initAD()` at line 19 and `initDigIO()` at line 54.

`initDigIO()` opens `brightness` files for two of the user LEDs in `/sys/class/leds`. We will use these in the next chapter.

`initAD()` is where you would normally expect to open a connection to the analog input file. But it turns out that the `open()` call triggers the A/D converter. I would have expected that to happen in `read()`, but it doesn’t. There appear to be mechanisms for triggering the A/D through `/sys`, but again it is not obvious. So, for now, `initAD()` is a dummy.

Reading the A/D converter is handled by the generically named `readAD()` function at line 30. It opens the analog channel file, reads one sample, closes the file, and returns the binary value.

Digital output is embodied in three functions: `setDigOut()`, `clearDigOut()`, and `writeDigOut()`. These functions simply write the appropriate text value, “0” or “1”, to the corresponding `brightness` file.

`closeAD()` is a dummy. `closeDigIO()` just closes the two `brightness` files.

The Makefile for the measure project has several build targets. By default, Eclipse only knows how to build the “all” target if it is present. In the case of the measure project, all builds something called a “simulation version”. We will talk about that in the next chapter. Other build targets require that they be declared to Eclipse. On the right-hand side of the C/C++ perspective is a view normally labeled Outline, that shows an outline of whatever is currently displayed in the Editor window. There is another tab in that view labeled Make Targets that allows us to specify alternate make targets. Select that tab, right click on the measure project, and click Add Target.

Fig. 7.8 shows the dialog brought up by Add Target. In this case, the Target Name is measure. The Make Target is also measure, so we do not have to retype it. Eclipse provides a shortcut for the common case when the target name and make target are the same. Click the create button. Now in the Make Targets view, under the measure project, right click on the measure target, and select Build Make Target. In the Project Explorer view on the left-hand side of the perspective, three new files show up: measure.o, trgdrive.o, and measure.

![](img/f03d6fa2c5faefc793771df52bbb2ef9_129_0.png)

**Figure 7.8**  
Create Make Target dialog.

Run the program on the target. Depending on which file you chose to open, the ADC returns either the 12-bit raw data in the range of 0 to 4095, or millivolt data in the range of 0 to 1800. Turn the pot with a small screwdriver, and you should see the reported value change appropriately.

In this chapter, we learned how to access the peripheral registers on the BBB target board, and a little about how to manage peripherals through the /sys file system. The next chapter will delve more deeply into the subject of debugging.

### Resources

- www.ti.com/lit/pdf/spruh73 - AM35xx and AMIC110 Sitara Processors Technical Reference Manual
- github.com/CircuitCo/BeagleBone-Black/blob/master/BBB_SRM.pdf - BBB System Reference Manual
- github.com/CircuitCo/BeagleBone-Black/blob/master/BBB_SCH.pdf - BBB schematics in PDF
- beaglebone.cameon.net/home/reading-the-analog-inputs-adc - Useful write up on accessing the BBB ADC.
- https://www.linux.com/learn/how-get-analog-input-beaglebone-black - Another take on the BBB ADC
- If you want to investigate the /sys file system in more detail (and you should), check these out:
  - beagle.s3.amazonaws.com/esc/sysfs-esc-chicago-2010.pdf
  - www.signal11.us/oss/udev/
  - www.kernel.org/pub/linux/kernel/people/mochel/doc/papers/ols-2005/mochel.pdf - this paper is a little old, but it is still a good read.
