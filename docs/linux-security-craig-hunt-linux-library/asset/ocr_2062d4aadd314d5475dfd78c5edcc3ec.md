# **The SOCKS5 IPv4-to-IPv6 Translator**

A little-known bonus that you get with the SOCKS5 reference implementation is the ability to bridge the gap between IPv4 and IPv6 hosts in your network. This is currently accomplished via a patch to the standard SOCKS5 server distribution, although NEC plans to eventually roll IPv6-to-IPv4 translation support in the standard SOCKS5 distribution.

The translator, named *Socks5-Trans*, functions by accepting both IPv4 and IPv6 requests, either on separate interfaces (as a multi-homed server) or on the same physical interface (in a single-home configuration). This effectively allows you to gradually roll IPv6 onto your network, while taking advantage of the security features that SOCKS5 provides.

Once you have downloaded and expanded the standard SOCKS5 package, you need to download the separate software patch that provides the translation service; at the writing of this book, this file is called socks5-trans-v1.3-patch.gz. Place the patch file in the main source directory of the package and proceed to unzip it and apply it as follows:

```
```
[ramon]$ ls  *patch*
socks5-trans-v1.3-patch.gz
[ramon]$ gunzip socks5-trans-v1.3-patch.gz
[ramon]$ ls  *patch*
socks5-trans-v1.3-patch
[ramon]$ patch -p < ./socks5-trans-v1.3-patch
```
```

This results in the modification of all the source code files necessary for IPv6 support and IPv4-to-IPv6 translation.