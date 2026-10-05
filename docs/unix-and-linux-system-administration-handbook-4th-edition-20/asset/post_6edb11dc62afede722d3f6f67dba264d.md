
# Chapter 27

# Data Center Basics

A final point to note on this topic is that estimating the amount of power you need in a data center (or to size a UPS), you should measure devices' power consumption with a clamp-on ammeter (aka current clamp) such as the Fluke 902 rather than relying on the manufacturer's stated values as shown on the label (which typically represent maximum consumption values).

# Remote control

You may occasionally find yourself in a situation which you need to regularly power-cycle a server because of a kernel or hardware glitch. Or, perhaps you have non-UNIX servers in your data center that are more prone to this type of problem. In each case, you may want to consider installing a system that lets you power-cycle problem servers by remote control.

A reasonable solution is manufactured by American Power Conversion (APC). Their MasterSwitch product is similar to a power strip, except that it can be controlled by a web browser through its built-in Ethernet port. You can reach APC at (401) 789-0204 or on the web at ap.com.

# 27.4 RACKS

The days of the traditional raised-floor data center—in which power, cooling-network connections, and phone lines are all hidden underneath the floor—are over. Have you ever tried to trace a cable that runs under the floor of one of these labyrths? Our experience is that while it looks through glass, a “classic” raised-floor room is a rat's nest. Today, you should use a raised floor to hide electrical power feeds, distribute cooled air, and for nothing else. Network cabling (both copper and fiber) should be routed through overhead raceways specifically for this purpose.

In a dedicated data center, storing equipment in racks (as opposed to, say, setting it on tables or on the floor) is the only maintainable, professional choice. The best storage schemes use racks that are interconnected with an overhead track system for routing cables. This approach confers irrespective high-tech feel without sacrificing organization or maintainability.

The best track system is manufactured by Chatsworth Products (Watts-CA, (818) 882-8595, chatsworth.com). Using standard 19”-single-rail telco racks, you can construct homes for shelf-mounted and rack-mounted servers. Two back-to-back 19” telco racks make a high-tech-looking “traditional” rack (for cases in which you need to attach rack hardware both in front and in back of equipment). Chatsworth provides the racks, cable races, and cable management doodads, as well as all the hardware necessary to mount them in your building. Since the cables lie in visible tracks, they are easy to trace and you will naturally be motivated to keep them tidy.

# 27.5 Tools

A well-outfitted sysadmin is an effective sysadmin. Having a dedicated tool box is an important key to minimizing downtime in an emergency. Table 27.3 lists some items to keep in your tool box, or at least within reach.

# Table 27.3 System administrator’s tool box

| General tools | |
|---|---|---|
| (Allen) wrench kit | Ball-pen hammer, 4 oz. |
| Scissors | Electrician's knife or Swiss army knife |
| Small LED flashlight | Phillips-flat screwdrivers: #0, #1, and #2 |
| Socket wrench kit | Pliers, both flat-needled and regular |
| Stud finder | Rigid Seesnake micro inspection camera |
| Tape measure | Slot-head screwdrivers: 1/8", 3/16", and 5/16" |
| Torx wrench kit | Teensy tiny jeweler's screwdrivers |
| Tweezers | |

| Computer-related specialty items | | |
|---|---|
| Digital multimeter (DMM) | Cable ties (and their Velcro cousins) |
| Infrared thermometer | PC screw kit (as those from crazypc.com) |
| RJ-45 crimper | Portable network analyzer/laptop |
| SCSI instruments | Spare Category 5 and 6A RJ-45 crossover cables |
| Spare power cord | Spare RJ-45 connectors (solid core and stranded) |
| Static grounding strap | Wire stripper (with an integrated wire cutter) |

| Miscellaneous | | |
|---|---|
| Can of compressed air | Dentist's mirror (possibly a telescoping one) |
| Cellular telephone | First-aid kit, including ibuprofen and acetaminophen |
| Electrical tape | Home phone and pager #s of on-call support staff |
| Q-Tips | List of emergency maintenance contacts |
| | Six-pack of good microbrew beer (suggested minimum) |

a. And maintenance contract numbers if applicable

# 27.6 Recommended Reading

Telecommunications Infrastructure Standard for Data Centers. ANSI/TIA/EIA 942.

ASHRAE Inc. ASHRAE 2008 Environmental Guidelines for Datacom Equipment. Atlanta, GA: ASHRAE, Inc., 2008.

EUBANK, Huston, JOEL SWISHER, CAMERON BURNS, JOEL SEAL, and BEN EMERSON. Design Recommendations for High Performance Data Centers. Snowmass, CO: Rocky Mountain Institute, 2003.

# 27.7 EXERCISES

- E27.1 Why would you want to mount your computers in a rack?

- E27.2 Environmental factors affect both people and machines. Augment the factors listed in this book with some of your own (e.g., dust, noise, light, clutter, etc.). Pick four factors and evaluate the suitability of them for lab and machine.

- E27.3 A workstation draws 0.8 A, and its monitor draws 0.7 A @ 120 V.
  a) How much power does this system consume in watts?
  b) With electricity going for about $0.12/kWh, what does it cost to leave this system on year-round?
  c) How much money can you save annually by turning off the monitor for an average of 16 hours a day (either manually or with Energy Star features as DPMS)?
  d) What is the annual cost of cooling this system? (State your assumptions regarding cooling costs and show your calculations.)

- E27.4 Design a new computing lab for your site. State your assumptions regarding space, numbers of machines, and type and power load of each machine. Then compute the power and cooling requirements for the lab. Include both servers and client workstations. Include the layout of the room, the lighting, and the expected human load as well.

# 28 Green IT

You might think that a book about system administration would be the last place to find environmental consciousness. But now large installations have started to attract attention. Green IT is the art and science of reducing these not-hidden costs. We focus on some basic concepts you can use to reduce your IT organization’s energy and resource consumption. We’ve targeted organizations that have 1 to 500 servers in their data centers. If your environment is larger, you should consider hiring an expert in green data-center construction to achieve the most drastic results.

# 28.1 GREEN IT INITIATION

Exactly does it mean to be “green”? We define it as

- Lower power consumption
- Smaller physical plant requirements
- Lower consumption of consumables
- Recyclable outputs

There is no silver bullet or single path to a green IT environment. Despite some vendors’ claims, you cannot purchase one product that makes all the greenness in the world show down upon you. Specifically, green IT is a lot more than server virtualization. And, like many aspects of system administration, green IT is more a journey than a destination. You must visualize where you want to go, map out a plan to get there, and chart your progress along the way. Ongoing measurement and monitoring must be key elements of your overall plan.

Start your green IT journey by assessing the eco-friendliness of your current environment. A comprehensive view of all IT within your organization, not only to maximize the project’s impact but also to ensure that you don’t end up playing the “squeeze the balloon” game. For example, it might seem eco-wonderful to remove all the servers from your environment until you discover that eliminating 50 managed servers has resulted in users purchasing and deploying 600 rogue server-class systems in their cubicles as part of a “personal server deprivation revolt.”

But why bother? Bragging rights and the satisfaction of doing the right thing for the planet may be reason enough for some. But there are practical reasons for decision-makers to consider a green IT effort as

- initial costs – by minimizing the equipment you buy, you reduce capital expenditures. By minimizing the size of the data center, you can reduce real estate.

- operating costs – power, management, and maintenance cost money over time. Efficient use of fewer pieces of equipment means less spent on operations.

- – you pay for electricity twice: once to power your equipment, and then again to cool down it.¹ Less equipment means less cooling, less square footage, and fewer people dedicated to IT operations.

> ¹ The informational work done by IT equipment is not significant in a thermodynamic sense. Computers are essentially
