that have been configured for device swap up to the maximum limit of 25. Only an integer value is allowed (formula values do not work for this parameter).

Description

`"nswapdev"` defines the maximum number of devices that can be used for device swap.

At system boot time, the kernel creates enough internal data structures to support device swap to the specified number of physical devices that have reserved system swap areas. If the specified value is greater than the number of available devices, the extra data structure space is never used, thus wasting a little bit of memory (<50 bytes per structure). If the value is less than the number of available devices, some devices cannot be used for swap due to lack of supporting data structures in the kernel.

Related Parameters

None.

# **nswapfs**

Specify number of file systems that can be enabled for file-system swap.

Acceptable Values:

+   Minimum:  `" 1"`
+   Maximum:  `" 25"`
+   Default:  `" 10"`

Specify an integer value equal to the number of file systems that are available for file-system swap up to the maximum limit of 25.

Description

`"nswapfs"` defines the maximum number of file systems that can be used for file system swap.

At system boot time, the kernel creates enough internal data structures (about 300 bytes per structure) to support file system swap to the specified number of file systems. If the specified value is greater than the number of available file systems, the extra data structure space is never used, thus wasting that much memory. If the value is less than the number of available file systems, some file systems cannot be used for swap due to lack of supporting data structures.