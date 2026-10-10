devices and/or file systems to improve system efficiency and minimize monopolization of a given device by the swap system.

# **swapmen_on**

Enable pseudo-swap reservation.

Acceptable Values:

Minimum: "0" (disable pseudo-swap reservation)

Maximum: "1" (enable pseudo-swap reservation)

Default: "1"

Specify integer value of "0" or "1".

# **Description**

"swapmen_on" enables or disables the reservation of
pseudo-swap, which is space in system memory considered as
available virtual memory space in addition to device swap space on disk.
By default, pseudo-swap is enabled.

Virtual memory (swap) space is normally allocated from the device
swap area on system disks. However, on systems that have massive
amounts of installed RAM and large disks or disk arrays, there may be
situations where it would be advantageous to not be restricted to the
allocated device swap space.

For example, consider an administrator running a system in single-user
mode that has 200 Mbytes of installed RAM, only 20 Mbytes of which is
used by the kernel, and 1 Gbyte of swap area on the root disk array.
Suppose a process is running that requires 1.1 Gbytes of swap space.
Since no other users have processes running on the system, providing
access to the unused RAM by the swap system would provide sufficient
swap space. "swapmen_on" accomplishes this.

Administrators of workstations and smaller systems may prefer to disable
this capability, depending on system and user needs.

# **timeslice**

scheduling timeslice interval

Acceptable Values:

Minimum: "-1"