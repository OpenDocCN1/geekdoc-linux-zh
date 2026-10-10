these networking topics, as opposed to the system administration aspect of them.

# ### /etc/hosts

This file contains information about the other systems to which you are connected. It contains the Internet address of each system, the system name, and any aliases for the system name. If the /etc/hosts file is modified to contain the names of the systems on your network, they have provided the basis for login to another system. Although you can now login to other UNIX systems, you cannot yet rcp or remsh to another system. Although adding remsh and rcp functionality is easy, it does indeed compromise security, so it is not always set up on all systems. Here is an example /etc/hosts file:

```
```
127.0.0.1localhostloopback
15.32.199.42a4410827
15.32.199.28a4410tu8
15.32.199.7a4410922
15.32.199.21a44410tu1
15.32.199.22a4410tu2
15.32.199.62a4410730
15.32.199.63hpxterm1
15.32.199.64a4410rd1
15.32.199.62a4410750hp1
```
```

This file is in the following format:

```
`<internet_address>          <official_hostname>  <alias>`
```

The Internet Protocol address (IP address) is a class “A,” “B,” or “C” address. A class “A” network supports many more nodes per network than either a class “B” or “C” network. The purpose of breaking down the IP address into four fields is to define a node (or host) address and a network address. Figures 9-3 through 9-6 described these classes in detail.

Assuming that the above /etc/hosts file contains class “C” addresses, the rightmost field is the host or node address, and the other three fields comprise the network address.

You could use either the official_hostname or alias from the /etc/hosts file when issuing one of the ARPA or Berkeley commands described earlier. For instance, either of the following ARPA commands work: