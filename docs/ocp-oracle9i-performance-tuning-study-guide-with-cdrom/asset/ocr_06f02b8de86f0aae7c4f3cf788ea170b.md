period, but declined to approximately 19MB by the end of the snapshot period. Ending Java Pool values that are near or steadily approaching zero indicate that the Java Pool may be too small.

# Improving the Performance of the Java Pool

When warranted by the query shown above, you can increase the size of the Java Pool by increasing the value for JAVA\_POOL\_SIZE in init.ora. The size of the Large Pool can be specified in bytes, kilobytes (using the K suffix), or megabytes (using the M suffix). The range of values for JAVA\_POOL\_SIZE is 1M to 1GB. The size of the Java Pool cannot be changed dynamically.

> **NOTE**
> If the Large Pool is configured, Java operations will make use of the Large Pool to store UGA information.

# Summary

Oracle9i includes several features that, if utilized, will impact the overall performance of the SGA structures. The Shared Server option is designed to allow you to add additional application users to an existing system without having to add additional CPU or memory resources to support those users. The Shared Server configuration accomplishes this by using Dispatchers and queuing to juggle incoming user requests between several available Shared Server processes instead of dedicating a Server Process to each user. Shared Servers and Dispatchers can both be monitored using dynamic performance views in order to determine whether there are enough of them available to service the user requests adequately. Additional Shared Server and Dispatcher processes can be started either manually or dynamically.

The Large Pool can be used to buffer UGA information for the Shared Server configuration as well as I/O related data for the RMAN, Parallel Query, and Database Writer I/O slaves options. The effectiveness of the Large Pool can also be analyzed by examining dynamic performance views, and its size adjusted accordingly.