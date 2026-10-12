![](bbox=[0.1, 0.08, 0.9, 0.33])

**Figure 15-9:** The distance of obstructive objects from the wireless signal is called the *clearance*.

+   * **Distance** — Although the actual distances over which antennas can send and receive data varies greatly based on different factors, you can achieve distances of many miles with outdoor antennas. For example, two Orinoco 24 dBi directional parabolic-grid antennas can theoretically achieve distances of up to 52 miles at an 11 Mbps transmission speed with a 180-meter clearance. Reduce that transmission rate to 1 Mbps and you can achieve distances of up to 149 miles with a 1200-meter clearance. Shorter distances are achieved with less expensive equipment, such as the Orinoco 14 dBi directional antenna which can achieve distances of up to 5.3 miles at 11 Mbps with a 13-meter clearance.

+   * **Cable factor** — The distances that transmissions travel on the cables between the wireless cards and the antennas can be a factor in choosing the right antenna. The shorter the cables, the greater the distance and speed you will get on your antenna.

The power of an antenna is rated in terms of *gain*. Gain is measured in decibels, based on a *theoretic isotropic radiator* (or *dBi*). Higher gains offer opportunities for reaching greater distances at greater speeds. However, the ability of the antenna to focus that power (directional versus omnidirectional), greatly affects the speeds and distances that can be achieved.

# Getting wireless drivers

If you are using a wireless card that includes a *supported driver in Fedora*, it's likely that it will be auto-detected and you will be able to configure it as described later in this section. However, using a Windows driver and the *ndiswrapper* driver requires some extra configuration. The following procedure contains an example of configuring *ndiswrapper* with a Linksys 802.11g wireless PCI adapter card.

> **NOTE:** Much of this procedure was from the *INSTALL* file that comes in the *ndiswrapper* package. You should check that file to make sure that the procedure hasn’t changed with the release of a new version of *ndiswrapper*.