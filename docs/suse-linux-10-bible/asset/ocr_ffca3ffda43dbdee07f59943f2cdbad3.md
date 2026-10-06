# 436 Part III ♦ Using the Command Line in SUSE Linux

# Listing 15-16: Using the traceroute Program to Diagnose Network Problems

```
thinkpad:~ # traceroute we.palcomoder.net
tracoute to www.palcomoder.net (212,132,208,115), 30 hops max, 40 byte packets
  192.168.1.1  2.734 ms  3.840 ms  3.231 ms
  2 217.441.132.74 17.986 ms  18.992 ms  19.735 ms
  3 217.441.132.11 21.366 ms  22.553 ms  24.021 ms
  4 217.441.132.106 30.135 ms  32.597 ms  33.552 ms
  5 194.106.131.36 34.500 ms  32.508 ms  34.052 ms
  6 194.106.132.11 29.242 ms  30.509 ms  31.278 ms
  7 195.66.226.103 30.782 ms  31.283 ms  32.833 ms
  8 194.151.169.25 34.975 ms  35.234 ms  37.647 ms
  9 212.131.195.93 39.701 ms  40.441 ms  41.401 ms
 10 212.133.210.60 41.606 ms  44.235 ms  45.992 ms
 11 oscan.palcomoder.net (212,132,208,115) 33.374 ms  30.918 ms
```

For each router `traceroute` passes, you see the router's IP address and timings. When the router is queried, the query actually happens three times to allow you to learn an average response time from the router.

# Wireless Networking

One of the best of the networking technologies that have come along in the past few years is wireless networking. Wireless networking is its quickest adoption in the laptop market, and many machines now use the Centrino chipset from Intel.

If your laptop does not include an onboard wireless chipset, you will probably find a good PCMCIA (an expansion slot for laptops) that provides wireless service for you. A lot of Linux users have great results with the Cisco wireless cards.

If you are not whether your wireless networking card is supported in Linux, or you are looking to purchase one, Google is always your friend. Use Google to search for the term "Linux" and the model number of the wireless networking card you are interested in.

Starting with SUSE 9.3 and in subsequent releases, SUSE has added a lot more support for the particular Centrino chipset. The firmware files for these chipsets are now included in the distribution and are configurable in the same way as a normal network card under YaST.