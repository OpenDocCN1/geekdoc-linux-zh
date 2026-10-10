This script shows that the cable on altiva is attached to `/etc/ttyS1`. Next, both scripts should be made executable and copied to the `/usr/local/bin` directory:

```
```bash
# chmod +x hook
# cp hook /usr/local/bin
```
```

Ensure that networking services are enabled on both machines, and connect the serial cable to the appropriate ports on each computer. Then, on each computer, execute this command:

```
```bash
# hook
```
```

You can then verify the connection by using the `ping` or `ifconfig` commands. Although this setup doesn't offer blistering networking speeds, it is a very cost-effective solution that works in a pinch.

# Networking with the Parallel Line Interface Protocol

The Parallel Line Interface Protocol (PLIP) is another inexpensive way to network two computers, but with better performance than using serial ports. You'll need a free parallel port on each computer (set to ECP, EPP, or bidirectional mode), along with a parallel null cable. Many shorter cables (6 feet or less) may be found at larger computer discount stores.

Your kernel must support loadable modules, networking, IP forwarding, network devices, the parallel port, and associated devices. This shouldn't be a problem for stock kernels from recent Red Hat or Mandrake Linux distributions.

Your notebook must also have at least a bidirectional parallel port. Although PLIP works well with many desktop computers, not all notebooks can support this protocol, because the parallel port does not work well bidirectionally (despite manufacturer and BIOS claims to the contrary).

Here is the general procedure to set up a PLIP link between two Linux computers, such as laptop to laptop or desktop to laptop:

Connect the cable to each computer. Next, boot each computer and check each one's parallel-port BIOS information. On each computer, make sure `/etc/hosts` contains the IP address of the two computers, and then issue this command:

```
```bash
# insmod parport
```
```

This loads generic support code. Next, load the parport_pc module with this:

```
```bash
# insmod parport_pc io=0x378 irq=7
```
```