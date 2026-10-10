+   * Minimum: “0”
+   * Maximum: none
+   * Default: “0”

Specify integer value.

# Description

On large systems, the time required to dump system memory when a kernel panic occurs can be excessive or even prohibitive, depending on how much physical memory is installed in the system. Fast-dump capabilities controlled by the “dontdump” and “alwaysdump” parameters provide a means for restricting kernel dumps to specific types of information:

+   * Unused Physical Memory
+   * Kernel Static Data
+   * Kernel Dynamic Data
+   * File-System Metadata
+   * Kernel Code
+   * Buffer Cache
+   * Process Stack
+   * User Process

The bit-map value stored in “alwaysdump” specifies which of these memory classes are to be included in the memory dumps associated with a kernel panic.

# Related Parameters

“alwaysdump” and “dontdump” have opposite effects. If the bit corresponding to a particular memory-page class is set in one parameter, it should not be set in the other parameter; otherwise a conflict occurs and the actual kernel behavior based on parameter values is undefined. These conflicts do not occur when SAM is used to set the values ([{Modify Page-Class Configuration}] in the [[Actions]] menu, SAM “Dump Devices” subarea in the kernel-configuration area).

# enable_idds

enable_idds is reserved for future use.

Acceptable Values:

Default: “0 (off)”