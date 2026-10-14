When applying an effect, the original file is never altered. You must specify an output file, or use a hyphen character (`-`) to indicate the standard output. Specify the output format as an argument to the `-t` option. You can only apply one effect with each `sox` command; thus, to add both echo and reverb to a sound file, you would need to issue two `sox` commands.

The amount and levels applied for each effect will vary with every situation. As such, consider the following recipes as guidelines only for using the options; you will probably end up experimenting a bit to achieve your intended effect for any particular sound file.

Almost all of the sound effects are applied by specifying the input and output file arguments, followed by the name of the effect to use and any options the effect takes (with notable exceptions, like the `-v` option for changing the amplitude of a file).

**NOTES:** For more information on the sound effects `sox` can apply, see the various files in `/usr/doc/sox/`, and read the `sox` man page (see Recipe 2.8.4 [Reading a Page from the System Manual], page 46).

# 23.2.1 Changing the Amplitude of a Sound File

To change the volume or amplitude of a sound file, use `sox` with the `-v` option, giving the volume level as an argument. Levels below 1.0 lower the amplitude, and higher numbers raise it.

⇒ Here are two ways to use this.

+   - To raise the volume of file `old.wav` twofold and write the output to `new.wav`, type:
+   
+     ```sh
+     $ sox -v3 old.wav new.wav
+     ```
+   
+   - To lower the volume of file `old.wav` by half and write the output to `new.wav`, type:
+   
+     ```sh
+     $ sox -v.5 old.wav new.wav
+     ```

Use `sox` with the stat option and `-v` to determine the largest possible value that can be used before distortion or clipping occurs (it performs a statistical analysis on the file and outputs a numeric value). This value comes in handy when you want to raise a file’s volume as high as possible without ruining its fidelity.