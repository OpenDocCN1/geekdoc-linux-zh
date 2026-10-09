We won’t list all the device drivers here, as there’s very little to be learned from such a list other than the hardware FreeBSD supported at the time I wrote this section. Check the release notes for the version of FreeBSD you’re running to see what hardware it supports.

You’ll also find a big section of drivers for virtualization. The most commonly used virtual interfaces are based on VirtIO, but you’ll also see specific drivers for Xen, Hyper-V, and VMware. A kernel needs only the drivers for the virtualization platform it’s run on. Kernels for real hardware don’t need any of them, even if the host will have virtual machines running on it.

# ## Pseudodevices

You’ll find a selection of pseudodevices near the bottom of the `GENERIC` kernel configuration. As the name suggests, these are created entirely out of software. Here are some of the more commonly used pseudodevices.

| device | loop | # Network loopback |
|:-------|:-----|:-------------------|

The loopback device allows the system to communicate with itself via network sockets and network protocols. We’ll discuss network connections in some detail in the next chapter. You might be surprised at just how many programs use the loopback device, so don’t remove it.

| device | random | # Entropy device |
|:-------|:-------|:-----------------|
| device | padlock_rng | # VIA Padlock RNG |
| device | rdrand_rng | # Intel Bull Mountain RNGdevice |

These devices provide pseudorandom numbers, required for cryptography operations and such mission-critical applications as games. Some of them require support in the underlying chipset. FreeBSD supports a variety of randomness sources, transparently aggregating them all into the random devices `/dev/random` and `/dev/urandom`.

| device | ether | # Ethernet support |
|:-------|:------|:------------------|