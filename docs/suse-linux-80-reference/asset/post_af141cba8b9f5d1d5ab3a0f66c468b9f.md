
For security reasons, only users belonging to the group **video** may access the 3D hardware. Verify that all users working locally on the machine are members of this group. Otherwise memory access errors will occur when attempting to start OpenGL applications (Nvidia-GLX) and the previous *Software Rendering Fallback* of the OpenGL driver will be used (DRI). Use the command `id` to check whether the active user belongs to the group *video*. If this is not the case, use YaST2 to add the user to the group.

## Mesa/Glide

This OpenGL driver needs to be manually configured with the help of the information provided by `3Ddiag`. Details can be found in Section *Diagnosis Tool 3Ddiag* on this page.

If you have a Mesa/Glide driver, start OpenGL applications as `root`, because only root can access the hardware. To allow this, the user currently logged in will have to enable `$DISPLAY` for root. This can be done with the command `xhost localhost`. The resolution used by the OpenGL application requires GLIDE support (resolutions supported are 640×480 and 800×600). Otherwise the very slow “Software rendering fallback” of the OpenGL driver will be used.

## Diagnosis Tool 3Ddiag

The diagnosis tool 3Ddiag is available for the purpose of verifying the 3D configuration in SuSE Linux. This is a command line tool that must be invoked inside a terminal.

The application reviews, for example, the XFree86 configuration to verify that 3D support packages are installed and the proper OpenGL library is used with the GLX extension. Follow the directions in 3Ddiag if "failed" messages appear. Ideally, you will only see "done" messages on the screen. Unless 3D support was already activated during installation, the 3D configuration of the Mesa/Glide OpenGL driver using this diagnosis can be relatively intensive.

`3Ddiag -h` provides information about options for 3Ddiag.

## OpenGL Test Applications

Games, such as `bzflag`, `tuxracer`, and `tuxkart` (from the packages with the same name) and `gears` and `glinfo` from the package `mesa`, are suitable as OpenGL test applications. If 3D support has been activated, they can be played well on a somewhat up-to-date computer. These games, however, are not recommended in conjunction with Mesa software rendering because of the resulting slide show effect.

## Troubleshooting

If the OpenGL 3D test results are negative (the games cannot be effectively played), use 3Ddiag to make sure no errors exist in the configuration ("failed" messages). If correcting these does not help or if failed messages have not appeared, take a look at the XFree86 log files. Often, you will find the line "DRI is disabled" in the XFree86 4.x file `/var/log/XFree86.0.log`. The exact cause can only be discovered by closely examining the log file — a task requiring some experience.

In such cases, it is common that no configuration error exists, as this would have already been detected by 3Ddiag. Consequently, at this point, your best bet is the Mesa software rendering OpenGL driver, which does not feature 3D hardware support. Take advantage of Mesa software rendering and forgo 3D hardware acceleration to avoid OpenGL representation errors or instability. A familiar example for the latter is the use of DRI and bttv (Watching TV in Linux) with ATI Rage 128 cards.

## Installation Support

Apart from Mesa software rendering, all OpenGL drivers in Linux are in developmental phases and are therefore considered experimental. The drivers are included in the distribution because of the high demand for 3D hardware acceleration in Linux. Considering the experimental status of OpenGL drivers, we cannot offer any installation support for configuring 3D hardware acceleration or provide any further assistance with related problems. The basic configuration of the graphical user interface X11 does not include 3D hardware acceleration configuration. This chapter answers many questions regarding this topic. If you have problems with 3D hardware support, use Mesa software rendering as already outlined in Section *Mesa Software Rendering* on page 170.

## Additional Online Documentation

- nVidia GLX: `/usr/share/doc/packages/nv_glx/`, `/usr/src/kernel-modules/nv_glx/README NVIDIA_GLX` and `NVIDIA_kernel` from the nVidia server
- DRI: `/usr/X11R6/lib/X11/doc/README.DRI` (package `xf86`, series x)
- Utah GLX: `/usr/share/doc/packages/glx/` (package `glx`, series x3d)
- Mesa/Glide: `/usr/share/doc/packages/mesa3dfx/` (package `mesa3dfx`, series x3d)
- Mesa general: `/usr/share/doc/packages/mesa/` (package `mesa`, series x3d)

## Joystick Configuration

USB port joysticks are automatically supported by SuSE Linux. Use the YaST2 module “Sound Configuration” to configure analog devices on the sound card’s joystick port.

Test your joystick using `jstest /dev/js0`. The command shows the joystick values that change when the joystick is moved or you press its buttons.

If necessary, calibrate the joystick using the jscalibrator (`/usr/bin/jscalibrator`) application from package libjsw, series d and package libjsw-calibrator, series d.

![](img/a4b6c994843f3fbd688003f4cabfa48f_184_0.png)

*Figure 7.14: Calibrating the Joystick*

This completes the configuration of your joystick. Your joystick is now ready to use. Try starting an application that supports the joystick as an input device, such as the game clanbomber, package clanbomber, series fun.

If you experience any problems, find additional configuration instructions and options for the different joystick modules in the file `/usr/src/linux/Documentation/input/joystick.txt`, package kernel-source, series d.

## Sound with ALSA

ALSA — http://www.alsa-project.org. The following sections are based on the fundamentals outlined in the Applications Manual.

- Basic PCM Types ........................................ 176
- The Mixer envy24control ............................... 177
- Compressing Audio Data ................................ 179
- Buffering and Latencies ................................ 180
- ALSA and MIDI ............................................. 181
- kmid — The MIDI Player ................................ 186
- Playing MIDI Files Without a WaveTable Card ..... 187
- arecord and aplay .......................................... 188

### Main PCM Types: hw and plughw

ALSA 0.9.x has changed and extended the concept of PCM devices. From now on, by selecting a given PCM type, the user can influence how ALSA accesses the sound card. The most important PCM types are hw and plughw.

To understand the difference between the two types, it is necessary to know how a PCM device is opened. Setting (at least) the following parameters is required: sample format, sample frequency, number of channels, number of periods (previously referred to as “fragments”), and size of a period. For example, an application may want to play back a WAV file with a sample frequency of 44.1 kHz, but the sound card does not support this frequency. In this case, ALSA automatically converts the data in the plug-in layer to a format the sound card supports. The conversion affects the parameters sample format, sample frequency, and number of channels.

Selecting the PCM type plughw activates the plug-in layer. Selecting the PCM type hw causes ALSA to attempt to open the PCM devices directly with the parameters required by the application.

The complete designator for a PCM device consists of the PCM type followed by a colon then the card number followed by the device number, for example:

`plughw:0,0`

### The Mixer for the Sound Chip Envy24

series snd, package alsa

![](img/a4b6c994843f3fbd688003f4cabfa48f_188_0.png)

*Figure 8.1: Monitor and Digital Mixer in envy24control*

envy24control is a mixer application for sound cards with the Envy24 (ice1712) chip. Start the mixer either with ‘SuSE’ → ‘Multimedia’ → ‘Sound’ or at the command line with envy24control &.

Next, we will describe the most important features in envy24control. The Envy24 chip’s flexibility also means that its functionality can differ depending on the sound card. Up-to-date and detailed information about the Envy24 sound chip can be found in `/usr/share/doc/packages/alsa/alsa-tools/envy24control`.

#### Monitor and Patchbay in envy24control

The signal controls are shown in the ‘Monitor Mixer’ in envy24control. The signals can be mixed in the sound card. The signals with the label ‘PCM Out’ are generated by applications, which send PCM data to the sound card. The signals of the analog inputs are shown under ‘H/W In’. The ‘S/PDIF’ input displays are shown to the right of this. Input and output controls for the analog channels must be set under ‘Analog Volume’.

Use the ‘Monitor Mixer’ sliders for the digital mixing. The controls for this are shown in ‘Digital Mixer’. The output routing of this mix is defined in the ‘Patchbay’. The ‘Patchbay’ contains a column of radio buttons corresponding to each output channel, which can be used to select the desired channel source.
