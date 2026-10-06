# 16.3 Implementation

```
ip_route_input_slow()
```

To begin with, an rt_key structure is filled with the parameters passed. However, before it is used to run a FIB query for invalid values-multicast source addresses,and moving a network prefix with null. Such packets are dropped, and if verbose messages are configured with CONFIG_IP_ROUTE_VERBOSE, they are registered in the system log. The use of 0.0.0.0 as source and destination addresses in the sense of limited broadcast is explicitly allowed as an exception, for this is occasionally used for automatic network configuration.

Next, the FIB query is started by fib_lookup(). If no matching entry is found, ip_route_input_slow() also aborts processing and returns an error code, which subsequently causes ip_rcv_finish() (from where ip_route_input_slow() was invoked) to discard the packet.

If the routing NAT mentioned in Section 16.1.6 is active, the next steps the source address according to the information in the routing used (or the destination, if the route is not nat). However, the new addresses are added only to the rt_key structure; the old addresses are maintained in the call parameters of the function and are available for other operations. The destination address has transformed, fib_lookup() has to be invoked once more to find a regular routing entry (no other transformations are permitted) to the destination address.

Among other things, the result from the FIB query also shows whether the destination address is a local address, which means that the packet is intended for the local system. This case is handled separately in the further process.

Local destination: A new cache entry is created once the source address has been checked by the calling of fib_validate_source(). The function pointer output() gets the ip_rt_bug() value, because the packet is not allowed to leave the system. Next, the input() pointer is set to ip_local_deliver(), to cause the packet to be delivered to the local machine. Because there is no router, the rt_gateway address of the cache entry is set to the destination address.

Broadcast addresses, such as the 0.0.0.0 mentioned above as source and destination the normally limited broadcast to 255.255.255.255 are detected in the address validation at the beginning and handled locally to local destination addresses. However, fib_validate_source() is not called for 0.0.0.0 addresses.

Nonlocal destination address: Nonlocal destination addresses have to be handled only if the forwarding function for the input interface is enabled, so this is checked first.

If the routing-table entry found describes several output routes, then fib_select_multipath() is called to select one of those routes. Subsequently, the source address is checked by the function fib_validate_source(), which can also consider the output network interface found in this case.

```
ip_forward() and ip_output() are set in the new cache entry for the input() and output() function pointers. The function rt_set_nexthop() does
```