# Chapter 27 Data Center Basics

A data center is composed of:

+   * A physically safe and secure space
* Racks that hold computer, network, and storage devices
* Electric power sufficient to operate the installed devices
* Cooling, to keep the devices within their operating temperature ranges
* Network connectivity throughout the data center, and to places beyond (enterprise network, vendors, Internet)

# 27.1 DATA CENTER RELIABILITY TIERS

Several aspects of a data center's design contribute to the overall availability it can provide, including

+   * Uninterruptible power supplies (UPSAs) – UPSs provide power when the normal long-term power source (e.g., the commercial power grid) becomes unavailable. Depending on size and capacity, they can provide anywhere from a few minutes to a couple of hours of power. UPS alone cannot support a site in the event of a long-term outage.
* On-site power generation - If the commercial grid is unavailable, on-site standby generators can provide long-term power. Generators are usually fueled by diesel, LP gas, or natural gas and can support the site as long as fuel is available. It is customary to store at least 72 hours of fuel on-site and to arrange to buy fuel from multiple providers.
* Redundant power feeds – In some locations, it may be possible to obtain more than one feed from the commercial power grid (possibly different from power generators).
* Mechanical systems – These are also known as HVAC systems, but in the context of a data center, only cooling is really relevant—no heat necessary! A plethora of available technologies provide both primary and standby cooling.

The Uptime Institute is an industry group that researches and guides data centers. They have developed a four-tier system for classifying the reliability of data centers, which we summarize in Table 27.1. In this case, N means that you have just enough of something (UPSs, generators) to meet normal needs. N+1 means that you have one spare; 2N means that each device has its own spare.

Centers in the highest tier are “compartmentalized,” which means that groups of systems are powered and cooled in such a way that the failure of one group has no effect on other groups.