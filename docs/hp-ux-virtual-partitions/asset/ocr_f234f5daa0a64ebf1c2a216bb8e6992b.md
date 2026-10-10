Default: `16`

Specify integer value.

# Description

This parameter defines the maximum number of streams modules that can be pushed onto any given stream. This provides some protection against run-away processes that might automatically select modules to push onto a stream, but it is not intended as a defense against malicious use of streams modules by system users.

Most systems do not require more than about three or four modules in any given stream. However, there may be some unusual cases where more modules are needed. The default value for this parameter allows as many as 16 modules in a stream, which should be sufficient for even the most demanding installations.

If your system needs more than 16 modules in a stream, the need should be carefully evaluated, and the demands on other system resources such as outstanding bufcalls and other factors should also be carefully evaluated.

# NSTRSCH

Set the maximum number of streams scheduler daemons (`smipsched`) that are allowed to run at any given time on the system.

Acceptable Values:

+   - Minimum: `0`
+   - Maximum: `32`
+   - Default: `0`

Specify integer value.

# Description

This parameter defines the maximum number of multi-processor (MP) streams-scheduler daemons to run on systems containing more than one processor. Note that uni-processor (UP) systems do not use an MP scheduler daemon, but both MP and UP systems always have one UP streams scheduler (`sopsched`).

If the parameter value is set to zero, the system determines how many daemons to run, based on the number of processors in the system. The value selected is `1` for 2-4 processors, `2` for 5-8 processors,