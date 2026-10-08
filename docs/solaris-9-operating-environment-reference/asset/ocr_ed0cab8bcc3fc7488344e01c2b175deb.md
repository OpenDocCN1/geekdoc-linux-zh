# 272

# dpost

Although dpost can handles files formatted for any device, emulation is expensive and can easily prepare the print time and the size of the output file. No attempt has been made to implement the character sets or fonts available on all devices supported by troff. Missing characters are replaced by white space, and unrecognized fonts usually default to one of the Times fonts (that is, R, I, B, or BI).

An rex command must precede the first init command, and all the input files should have been prepared for the same output device.

Note - Use of the -T option is not encouraged. Its only purpose is to enable the use of other PostScript font and device description files that, perhaps, use different resolutions, character sets, or fonts.

Although level 0 encoding is the only scheme that has been thoroughly tested, level 2 is fast and may worth a try.

# Options

+   -c num Print copies of each page. By default, only one copy is printed.
Set the text encoding level to num The recognized values are 0, 1, and 2. The size of the output file and print time should decrease as num increases. Level 2 encoding typically is about 20 percent faster than level 0 (the default) and produces output essentially identical to previous versions of dpost

+   -F dir Use dir as the font directory. The default dir is /usr/lib/font, and dpost reads binary font files from directory /usr/lib/font/devpost.

+   -H dir Use dir as the host-resident font directory. Files in this directory should be PostScript font descriptions. They must be assigned to the appropriate two-character troff font name. Each file is copied to the output file only when needed and at once during each job. There is no default directory.

+   -L file Use file as the PostScript prologue. The default is /usr/lib/lp/postscript/dpost.ps.

+   -m num Magnify each logical page by the factor num Scale pages uniformly about the origin, which is located near the upper-left corner of each page. The default magnification is 1.0.

+   -n num Print logical pages on each piece of paper, where num can be any positive integer. By default, num is set to 1.

+   -O Disable PostScript picture inclusion. A recommended option when running dpost by a spooler in a networked environment.