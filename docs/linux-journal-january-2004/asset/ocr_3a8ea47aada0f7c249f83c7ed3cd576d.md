xephem provides a software ephemeris, or sky charting interface, for the rest of the Talon suite. As with other ephemerides, it relies heavily on correct geographical and time coordinates; this information can be configured manually by the user. xephem also can be configured to poll an attached GPS at regular intervals, adjusting the system time to account for internal clock drift.

The xephem program, launched from the command line with xephem, provides a granular view of the current sky. Data on each object is provided in a right-click pop-up screen. The user also can point the telescope using this pop-up, a feature used extensively for calibration. Magnification can be increased, effectively looking deeper and deeper into the sky. As an alternative to zooming, the user may select a minimum magnitude (apparent brightness) threshold. This allows brighter stars to be filtered in the ephemeris view, leaving only the dimmer objects in the window. The sky view also may be rotated, and object type filtering is provided. For example, globular clusters can be selected, eliminating the view of all other object types.

# Configuration

Configuration files are critical to the operation of Talon. They provide the means by which the software communicates with both the user and the hardware installed in the telescope. In the Linux tradition, these files are simple text files, commented heavily for the clarification of the user. The configuration files for all elements of Talon can be found in /usr/local/telescope/archive/config. Using the default tcsh shell, the simple command cd config moves the user into the configuration directory.

The operation of the telescope can be viewed as two discrete elements, each of which is addressed by a specific configuration file type. First, the internal motion control boards must communicate with the motors and encoders. Configuration files intended to serve this function utilize a .cmc extension. I've always viewed this extension as delineating files that configure motion controllers, cmc for short. The .cmc files establish the operating parameters for the controller boards, which, in turn, send signals to and receive feedback from the encoders

and electromechanical components. The other element of telescope operation is the interface between the user and the software. In simple terms, all user-controlled operations utilize configuration files with a more traditional .cfg extension. Whereas the .cmc files operate behind the scenes to communicate directly with the hardware, the user interface must communicate with the .cfg files.

# Critical Configuration Files

Although every configuration file plays a role in the operation of Talon, some in both the .cmc class and the .cfg class bear special attention. These .cmc files include:

+   - basic.cmc: establishes the basic communication between the motion control boards and the motors driving the telescope axes.
- find.cmc: establishes the routines for finding objects based on encoder counts.
- nodeDec.cmc: establishes the hardware parameters for the Dec axis of the telescope.
- nodeRA.cmc: establishes the hardware parameters for the RA axis of the telescope.
- nodeFocus.cmc: establishes the hardware parameters for the telescope focus control.

The .cfg files are:

+   - boot.cfg: allows the user to script Talon startup routines. These may include starting GPS monitoring, weather station monitoring and opening the Talon main interface when the computer boots.
- home.cfg: provides an initial set of constants to allow the telescope to find the home position of each encoder. These constants represent a spatial sense for the telescope prior to working through the initial calibration routines. Once these routines are completed, the actual encoder counts and axis travel are updated automatically.

# Expand! $125

![](bbox=[0.67, 0.06, 0.92, 0.18])

# RouterBOARD 24

Four ethernet ports in one card that work as separate interfaces. Supported by all OSs!

# Combine! $195

![](bbox=[0.67, 0.28, 0.92, 0.42])

# RouterBOARD 230

A super small integrated motherboard with various interfaces and 266 MHz CPU. Use as a CPE or an AP on a tower with 500ft of PoE (802.3af), or anything else you can imagine! Many cases and accessories available. IDE/CF, PCMCIA, miniPCI, PCI, USB.

# route! $45

![](bbox=[0.67, 0.57, 0.88, 0.67])

# MikroTik.com RouterOS

A router operating system that has every possible feature a router could need - works with regular pc's and routerboards!

# more!

Four-port miniPCI to PCI $95
One-port miniPCI to PCI $33
v.35 synchronous miniPCI $550
and much more on ...

# RouterBOARD.com

sales@routerboard.com