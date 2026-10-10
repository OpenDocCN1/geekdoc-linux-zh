Description

Enter the value in bytes.

“maxdsiz” and “maxdsiz_64bit” define the maximum size of the data storage segment of an executing process for 32-bit and 64-bit processes, respectively.
The data storage segment contains fixed data storage such as statics and strings, as well as dynamic data space allocated using “sbrk()” and “malloc()”.

Increase the value of “maxdsiz” or “maxdsiz_64bit” only if you have one or more processes that use large amounts of data storage space.

Whenever the system loads a process, or an executing process attempts to expand its data storage segment, the system checks the size of the process’s data storage segment.

If the process’ requirements exceed “maxdsiz” or “maxdsiz_64bit”, the system returns an error to the calling process, possibly causing the process to terminate.

# max_fcp_reqs

Define the maximum number of concurrent Fiber-Channel FCP requests that are to be allowed on any FCP adapter installed in the machine. Acceptable Values:

Minimum: “ 0”
Maximum: “ 1024”
Default: “ 512”

Specify integer value or use integer formula expression.

Description

“max_fcp_reqs” specifies the maximum number of concurrent FCP requests that are allowed on an FCP adapter. The default value specified when the system is shipped is 512 requests. To raise or lower the limit, specify the desired value for this parameter. The optimal limit on concurrent requests depends on several different factors such as configuration, device characteristics, I/O load, host memory, and other values that FCP software cannot easily determine.

# Related Parameters and System Values