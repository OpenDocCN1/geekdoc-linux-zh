This is shorthand for “use a 24-bit netmask”, i.e. the netmask opposite the “/24” shown in the table; therefore the specification above means “IP address = 192.0.2.181, netmask = 255.255.255.0”

This is often referred to as the “CIDR notation” for netmasks or IP address ranges

+   5. “/32” specifies a single IP address. For example, 192.0.2.7 / 32 means this single machine – a range of length 1. You will never use this when configuring the IP address and sub-netmask of a machine on the LAN, but you will see it in routing tables and the like

+   6. “/0” or mask 0.0.0.0 specifies the whole Internet – every possible IP address – because it gives the same network part of 0.0.0.0 when combined with any IP address whatever. Again, you will see this in practice in routing tables, on Linux and NT, in the next chapter. (In some contexts “0.0.0.0” may be written as the word default instead, to emphasize that it means “every address”)

+   7. The 0-bits in the mask correspond to the host part of the address, which determines the network size. You can see graphically from the table that the network size gets bigger as you go down the table

+   8. It’s very important to note that the netmask on its own doesn’t specify the network. The netmask determines the size of the range, and the IP address positions it – saying where in the whole universe of IP addresses the range lies. It’s only the combination of netmask and the particular IP address that specifies the range uniquely. The table below shows four different ranges all of which have the same netmask (255.255.255.192):

| Address range | Range of last byte |
| :--- | :---: |
| 192.0.2.0–192.0.2.63 | 0–63 |
| 192.0.2.64–192.0.2.127 | 64–127 |
| 192.0.2.128–192.0.2.191 | 128–191 |
| 192.0.2.192–192.0.2.255 | 192–255 |

As you become more experienced in using netmasks you’ll get used to the start and end numbers of the common ranges.

> Tip: to work out how many addresses are in a range, subtract the last byte of the netmask from 256. For example, for netmask 255.255.255.224: (256 − 224) = 32-address network/range size. (This works only where the first three bytes are all 255. For other netmasks look up the size in the table.)