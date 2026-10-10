Another way to assign an IP address and enable the first Ethernet interface would be to use this:

```
# ifconfig eth0 valo up
```

In the first example, the `ifconfig` command is used to assign a specific IP address to eth0 and then activate the interface, or bring it “up.” The second example shows that you can also use information listed in your system’s /etc/hosts file, such as a hostname (such as valo) and its associated IP address to configure the interface. A small /etc/hosts file might look like this:

```
127.0.0.1             localhost             localhost.localdomain
192.168.1.2           wireless.home.org     wireless
192.168.2.30          valo.home.org         valo
192.168.2.31          aptiva.home.org       aptiva
192.168.2.32          ascentia.home.org     ast
192.168.2.33         stinkpad.home.org     stinky
```

To check on the status of an individual device, use `ifconfig`, followed by the device name, like this:

```
# ifconfig eth0
```

Apple iBook users might see something like this:

```
eth0          Link encap:Ethernet  HWaddr 00:04:27:AD:9C:DB
          inet addr:192.168.2.39  Bcast:192.168.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:30 errors:0 dropped:0 overruns:0 frame:0
          TX packets:33 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0
```

Intel-based notebook Linux users might see something like this:

```
eth0          Link encap:Ethernet  HWaddr 00:E0:98:06:84:C5
          inet addr:192.168.2.38  Bcast:192.168.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:46778 errors:0 dropped:0 overruns:0 frame:0
          TX packets:48398 errors:0 dropped:0 overruns:0 carrier:0
          collisions:4872 txqueuelen:100
          Interrupt:3  Base address:0x300
```

Note that the output of the `ifconfig` command is roughly the same in these two examples, with the exception of IRQ and I/O address information for the Intel notebook (the iBook uses different hardware and a different type of adapter).