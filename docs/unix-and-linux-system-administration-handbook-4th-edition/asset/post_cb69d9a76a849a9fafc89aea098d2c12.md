
## Table 27.2 Power-tier model for racks in a data center

| Power tier | Watts/rack |
|---|---:|
| Ultra-high densityᵃ | 25 kW |
| Very high density (e.g. blade servers)ᵇ | 20 kW |
| High density (e.g. 1U servers) | 16 kW |
| Storage equipment | 12 kW |
| Network switching equipment | 8 kW |
| Normal density | 6 kW |

ᵃ Projected top tier in 2015  
ᵇ Current top tier in 2010

The power allocations for the upper tiers in Table 27.2 may seem generous, but they are not so hard to reach, even with today’s equipment. APC measured the power consumption of a chassis containing 14 IBM BladeCenter HS20s at 4,050 watts.³ Six of those chassis in a rack consume 24.3 kW. Without cooling, that’s enough power to reduce 50 pounds of steel, aluminum, or silicon to a liquid puddle within 15 minutes. Needless to say, you’ll need special cooling arrangements and multiple power supplies for these configurations.

Once you’ve defined your power tiers, estimate your need for racks in each tier. On the floor plan, put racks from the same tier together. Such zoning concentrates the high-power racks and lets you plan cooling resources accordingly.

## kVA vs. kW

One of the many common disconnects between IT folks, facilities folks, and UPS engineers is that each of these groups uses different units for power. The amount of power a UPS can provide is typically labeled in kVA (kilovolt-amperes). But computer equipment and the electrical engineers that support your data center usually express power in watts (W) or kilowatts (kW). You might remember from fourth grade science class that watts = volts × amps. Unfortunately, your fourth grade teacher failed to mention that watts is a vector value, which for AC power includes a “power factor” (pf) in addition to volts and amps.

If you are designing a bottle-filling line at a brewery that involves lots of large motors and other heavy equipment, ignore this section and hire a qualified engineer to determine the correct power factor to use in your calculations. For modern-day computer equipment, you can cheat and use a constant. The equations you can use for a “probably good enough” conversion between kVA and kW are

```
kVA = kW / .85
kW = kVA * .85
```

³ See the white paper “Power and Cooling for Ultra-High Density Racks and Blade Servers” at apc.com.

A final point to note on this topic is that when estimating the amount of power you need in a data center (or to size a UPS), you should measure devices’ power consumption with a clamp-on ammeter (aka current clamp) such as the Fluke 902 rather than relying on the manufacturer’s stated values as shown on the label (which typically represent maximum consumption values).

## Remote control

You may occasionally find yourself in a situation in which you need to regularly power-cycle a server because of a kernel or hardware glitch. Or, perhaps you have non-UNIX servers in your data center that are more prone to this type of problem. In either case, you may want to consider installing a system that lets you power-cycle problem servers by remote control.

A reasonable solution is manufactured by American Power Conversion (APC). Their MasterSwitch product is similar to a power strip, except that it can be controlled by a web browser through its built-in Ethernet port. You can reach APC at (401) 789-0204 or on the web at apc.com.

## 27.4 RACKS

The days of the traditional raised-floor data center—in which power, cooling, network connections, and phone lines are all hidden underneath the floor—are over. Have you ever tried to trace a cable that runs under the floor of one of these labyrinths? Our experience is that while it looks nice through glass, a “classic” raised-floor room is a hidden rat’s nest. Today, you should use a raised floor to hide electrical power feeds, to distribute cooled air, and for nothing else. Network cabling (both copper and fiber) should be routed through overhead raceways designed specifically for this purpose.

In a dedicated data center, storing equipment in racks (as opposed to, say, setting it on tables or on the floor) is the only maintainable, professional choice. The best storage schemes use racks that are interconnected with an overhead track system for routing cables. This approach confers that irresistible high-tech feel without sacrificing organization or maintainability.

The best overhead track system is manufactured by Chatsworth Products (Chatsworth, CA, (818) 882-8595; chatsworth.com). Using standard 19" single-rail telco racks, you can construct homes for both shelf-mounted and rack-mounted servers. Two back-to-back 19" telco racks make a high-tech-looking “traditional” rack (for cases in which you need to attach hardware both in front of and in back of equipment). Chatsworth provides the racks, cable races, and cable management doohads, as well as all the hardware necessary to mount them in your building. Since the cables lie in visible tracks, they are easy to trace and you will naturally be motivated to keep them tidy.
