I divided the commands in the preceding script into six sections. The following text describes each of those sections.

# (1) Policies

The `iptables -P` commands set the default policies for `INPUT`, `OUTPUT`, and `FORWARD` chains. By assigning each of those policies to `DROP`, any packet that isn't matched is discarded. In other words, for a packet to get through, it has to be specifically matched and `ACCEPT`ed by one of the other rules in the script.

# (2) User-Defined Chain

A user-defined chain I call `okay` is created to do a few more checks on packets requesting certain `TCP` services that I'm going to allow through (Web, `FTP`, and `DNS` services). The `-N okay` option creates the `okay` chain. The next line says that a `SYN` packet (`- syn`), which requests a new connection, is fine to let through. The next line allows through packets associated with an `ESTABLISHED` connection (one that has already had traffic pass through the interface) or a `RELATED` connection (one that is starting a new connection related to an already established connection). The final line in this set tells `iptables` to `DROP` packets that don't meet one of those checks.

# (3) INPUT Chain Rules

The bulk of the packet filtering is done in the `INPUT` chain. The first set of input rules indicates to `iptables` when to always accept packets from the Internet and from the LAN. The next three sets determine which requests for specific protocols (`TCP`, `UDP`, and `ICMP`) are accepted:

+   * **Packets from LAN** — Because you want the users on your LAN and the firewall computer itself to be able to use the Internet, this set of rules lets through packets that are initiated from those computers. The first line tells `iptables` to accept packets for ALL protocols for which the source is an acceptable address on your LAN (`-s 10.0.0.0/24`, which represents IP numbers `10.0.0.1` through `10.0.0.254`). The next three lines allow packets that come from all valid IP addresses on the firewall itself (`-s 127.0.0.1, 10.0.0.1` and `123.45.67.89`). The last line accepts broadcast packets (`-d 10.0.0.255`) on the LAN.

+   * **Packets from Internet (Already Connected)** — This line is split in two (I just used the backslash to join the lines because the page wasn't wide enough to show it as one line). It `ACCEPTS` packets that are both associated with connections that are already established (`-state ESTABLISHED,RELATED`) and are requested directly to the firewall's IP address (`123.45.67.89`).

+   * **TCP Rules (New Connections)** — Here is where you open up the ports for the `TCP` services you want to provide to anyone from the Internet. In these lines you open ports for `FTP` service (`-destination-port 21`), secure shell service (22), `DNS` if you need to offer zone transfers (53), Web Service (80), and `IDENT` authentication (113), the last of which might be necessary for protocols such as `IRC`. Instead of accepting these requests immediately, you jump to the `okay` chain you defined to further check that the packets were formed properly.