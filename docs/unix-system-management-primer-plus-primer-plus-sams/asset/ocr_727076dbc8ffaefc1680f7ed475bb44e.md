# Chapter 9 • PREPARING FOR DISASTER RECOVERY

# Be Prepared—Even at Home

As the system administrator for your organization, you probably have some form of home access to your business network. If, your disaster preparedness plan needs to incorporate provisions for power outages at your home as well as your data center. Uninterruptible power supplies (UPS) and even small generators might be part of that plan. Make sure all essential equipment located in your home is equipped with adequate surge protection, to avoid surge damage from lightning or power restoration.

Residential power outages might seem insignificant when compared to large data centers with UPSs, stacks of batteries, and huge generators. By minimizing the inconvenience and loss of any type of power outage involves the same basic approach: having emergency equipment and supplies available and using a planned procedure for minimizing damages from the power outage. The same type of planning and execution can help minimize power-outage damage to your production infrastructure, as well, but it requires a great deal more thoroughness and documentation.

Power outages can occur from a variety of man-made and natural disasters, including storms, floods, and poorly planned digging with backhoes. Power company maintenance can interrupt service, as can temporary system overloads. Some outages are even planned and scheduled, as was the case with California's rolling blackouts in the summer of 2001. Although you can't predict the causes of power loss, you can plan for steps to minimize its effect on your systems.

# Potential Damage from Power Outages

A power outage can cause damage to your infrastructure on many fronts. The most obvious and immediate damage is that your systems no longer function, but this damage is remedied after power is restored. However, there are more severe consequences that a power outage can have for your systems, as follows:

+   - Sensitive electronic components can be damaged due to the surge after power is restored, rendering individual components or systems useless.
- If power is lost before a system has a chance to flush its pending writes to disk, the system loses data. If the data is critical operating system data, your system may not boot when power is restored.
- Magnetic tapes that are currently being read or written by a tape drive may get stuck in the drive when it abruptly stops. This often requires vendor maintenance and/or replacement of the drive.

![](bbox=[0.115, 0.07, 0.185, 0.115])