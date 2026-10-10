forever; you must terminate it by typing CTRL-C. The second command plays back the file you've just recorded, so you can check to see that it recorded correctly.

**Caution** Your mixer's audio gain settings can be extremely important when recording a file. If set too high, loud sounds will reach plateaus at the maximum values you can record, which results in a static-filled distortion. If set too low, the sound may be inaudible unless you adjust your playback volume settings upward. Using GUI tools and editors can sometimes help by providing a visual display of recording levels.

# ## GUI Audio Playback and Recording Tools

The play program is a very basic recording program. The program provides little in the way of feedback about a recording in progress, and of course as a text-mode program, it's not appealing to less experienced users. One solution is a simple X-based audio recorder, such as the GNOME Sound Recorder (shown in Figure 27-3). This program has capabilities similar to those of play, but it provides a GUI interface. You can launch the program by typing grecord at an xterm prompt or by selecting the program from the GNOME menus. KDE provides a similar tool, krecord, which you can launch by typing krecord at an xterm prompt or selecting the program from the KDE menus. You can record a file by clicking the Record button, play it back by clicking Play, and save it by selecting File \| As from the menu. You can adjust various recording options, such as the sample rate and number of channels, by selecting Settings \| Preferences. This action produces a dialog box in which you can set many of the options you can set in play/record via its command-line switches.

More sophisticated GUI audio tools, such as glame, xvave, and Sweep provide the means to edit an audio file. Figure 27-4 shows a Sweep editing window. This window displays the sound file visually—time runs from left to right, and the volume of the sound is represented by the magnitude of the sound waves in the editing window.

![](bbox=[0.13, 0.64, 0.93, 0.88])

Figure 27-3. Simple GUI audio playback and recording utilities provide few options, but are adequate for simple playback or recording tasks.