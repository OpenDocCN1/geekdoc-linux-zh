physical memory configuration that exceeds 1 Gbyte could potentially

deplete this reserve pool.

Depending on the exact nature of applications running on the system,

system load, memory and I/O configurations, and other factors, the

reserve pool could still become exhausted. If this happens, the

system prints a message to the console indicating that the reserve

pool has been exhausted and that “eqmemsize” should be increased.

# executable_stack

Allows or denies program execution on the stack (security feature).

Acceptable Values:

Minimum: “ 0”

Maximum: “ 2”

Default: “ 1”

Specify integer value. “0” is disable, “1” is enable, “2” is

enable with warning.

Description

executable_stack provides protection against commonly attempted

security breaches. It sets the system-wide default for whether to use

system memory-mapping hardware to help protect against one of the most

common classes of security breaches, commonly known as ‘stack buffer

overflow attacks.”

Unless you have a proven need to do otherwise, HP strongly recommends

that you set this parameter to a value of ‘0’ (zero). This is the

most secure of the settings, incurs no performance penalty, and will

very rarely interfere with legitimate applications.

Note that, for compatibility reasons, the default setting of this

parameter in this release is ‘1’ (one), which is the most compatible

but least secure setting. It is equivalent to system behavior on

HP-UX 11.00 and earlier, and does not provide protection against this

type of attack.

Refer to the description of the ‘+es’ option in the manual page for

charr(1) for a detailed description of the effects of this parameter, the

meanings of the possible settings, how to recognize if a different

setting may be needed on your system, and how to combine system-wide

and per-application settings for the best tradeoffs between security

and compatibility for your system.