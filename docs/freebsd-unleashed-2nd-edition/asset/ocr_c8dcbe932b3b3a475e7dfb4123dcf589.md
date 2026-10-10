# LISTING 23.1  Continued

```
```
set phone PHONE_NUM
set authname USERNAME
set authkey PASSWORD
set ifaddr 10.0.0.1/0 10.0.0.2/0 255.255.255.0 0.0.0.0
add default HISADDR  # Add a (sticky) default route
```
```

Here is what the various options mean:

+   - **set device**—This option should point to the device name that your modem is on. Here is a list of the DOS equivalents: COM1: `/dev/cuaa0`, COM2: `/dev/cuaa1`, COM3: `/dev/cuaa2`, COM4: `/dev/cuaa3`.

+   - **set log**—This option controls what types of events get logged, and it can be useful for debugging connection problems. This option will be covered more in the section on troubleshooting.

+   - **set speed**—This option sets the speed at which the serial port should run. The default setting of **115200** will work for most people. If you have problems with this on an older system, you may want to change it to **57600**.

+   - **set dial**—This option is the modem control string for the dialer. It is similar to the chat script used for kernel PPP. The default script will work for most people, so don't change this setting unless you have problems or are familiar with your modem's command set.

+   - **set ifaddr**—The part of the first number (**10.0.0.1/0**) that precedes the slash should be replaced with the IP address assigned to you by your ISP. If you have a dynamic IP address, leave the number as-is. The second number (**10.0.0.2/0**) should be replaced by the gateway address your ISP gave you. If your ISP has not given you a gateway address, leave this number as-is. The third number (**255.255.255.0**) is the netmask. Unless your ISP has given you a netmask number that differs from this number, you should leave this number as-is. For instance, a customized **ifaddr** line might look like this:

```
```
set ifaddr 64.41.131.102/0 64.41.131.1/0 255.255.255.0 0.0.0.0
```
```

+   - **set timeout**—The number here is the number of seconds of inactivity (no outgoing or incoming traffic) that will pass before the connection is terminated. It is similar to the **idle** option in kernel PPP.

+   - **set default HISADDR**—This line adds a default route to the routing tables for your ISP's gateway. Note that this line must appear after the **set ifaddr** line; otherwise, PPP will not know what the gateway address is.