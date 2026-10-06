
# Journaling File Systems

A journaling (also called logging) file system is a file system that writes metadata changes to a special log region on disk before writing them to their final destinations. File metadata is information about it, such as ownership, permissions, and modification times. When this data is corrupted or not updated properly—as would occur during a power failure—a file can become irrecoverably damaged. By writing this to a log first, journaling systems ensure a record exists for every metadata change before the actual file is updated. These records are removed from the log region only after they are successfully applied to the file. This system helps maintain file integrity at all times, while the log keeps records of changes that can be replayed later if the system is shut down unexpectedly. Some popular journaling systems include UFS (Solaris 8 and later), VxFS (Veritas File System), ext3/ext4 (Linux), JFS (AIX and Linux), and ReFS (Linux).

![](img/894492738e879267320b8d6f9a044180_243_0.png)

Power outages also cause problems beyond individual systems. Many people take climate control systems—heat, air conditioning, and humidity controls—for granted, but administrators know that proper atmospheric conditions in the data center are essential to keeping system equipment running safely and at peak capacity. Without adequate air conditioning, system hardware continually recirculates uncooled air through its cooling mechanisms. With each pass, the air becomes warmer; eventually, the air becomes so warm that it heats—rather—rather than cools—the hardware. The heat causes sensitive components such as CPUs to fail.

If a data center goes without heat in exceptionally cold weather, the equipment can grow too cold and condensation develop within the machines. Because computer equipment generates so much heat, data centers rarely grow too cold for the equipment to function efficiently. However, such cases have occurred.

HVAC failures can happen for any number of reasons, but one of the most common causes that is neglected is a power outage (you learn about HVAC equipment failures later in this chapter). In the worst-case scenario, a power outage occurs on a hot and humid day; the temperature in an improperly cooled running data center can quickly rise to 100°F.

![](img/894492738e879267320b8d6f9a044180_243_1.png)

# HVAC Draw on Emergency Power Supply

Generators can provide emergency power for your HVAC system, but even the smallest air conditioner consumes enormous amounts of electrical power, and few generators can power a large central HVAC system. Remember to take extra power consumption into account when researching redundant power sources.

# Providing Uninterruptible Power Supplies (UPSs)

Installing an uninterruptible power supply, or UPS, is the most convenient and cost-effective measure for minimizing losses resulting from power outages. A UPS protects against surges and other power irregularities, and it provides reliable battery backup in case of total power loss (see "Securing Uninterruptible Power Supplies," in Chapter 2, "Designing the Data Center Infrastructure," for more details). Because most power outages last only a few minutes, a UPS is usually sufficient to keep your systems up and running during typical power failures.

When power outages occur, however, you have no way of knowing if they'll last for a few minutes or a few hours. That's why a UPS serves another valuable purpose when power supplies fail. The UPS provides a buffer of battery power that transfers to another power circuit or physical location, or call the data center help desk to report the problem. During the outage, and when power eventually comes back on, the UPS will protect your valuable equipment from spikes that could otherwise fry your systems.

Many UPS are equipped with serial ports that you can connect to a server. The UPS uses this connection to report statistics such as battery power levels and load, but you can also use it to script the UPS using special software, like APC's PowerChute® (http://www.appc.com/products/powerchute_business_edition/index.cfm). The most powerful feature of this software is its ability to gracefully shut down the attached server (or even networks of servers) when battery life reaches a certain threshold (typically 3 minutes). This saves you the arduous task of manually shutting down each of your servers to avoid data loss or hardware damage. PowerChute can also notify an administrator via email when power supply is lost.

No UPS can replace power supplies for any length of time, however. Depending on the system's load, the battery on a UPS could last anywhere from a few minutes to several hours—long enough to perform backup and shut down, but not long enough to continue operating for days.

![](img/894492738e879267320b8d6f9a044180_244_0.png)

# System Administrators Should Have Laptops

Assuming your budget allows for it, purchase a laptop for yourself and other system administrators in your organization. A laptop allows you to work in any location with or without power. Because most residential phone lines do not run on the same power as the rest of your home, you should be able to dial in and perform emergency work even during a power outage.

To ensure that your IT department has a sound UPS plan, you can run tests to assess the capacity of your UPS and for how long it can provide that capacity after power is lost. If the capacity is unsatisfactory, consider purchasing additional batteries or upgrading to a higher capacity UPS.

![](img/894492738e879267320b8d6f9a044180_244_1.png)

# Shut Down Noncritical Systems

Identify systems on each UPS that are not critical during a power outage. Shutting these systems during a power outage reduces the load on the UPS and provides more uptime for the systems that are critical.

# UNIX SYSTEM MANAGEMENT PRIMER PLUS

Depending on your data center, you may have to supply your own UPS, or your provider might have battery backup on all of the power circuits already. Having your UPS never hurts, but it's an expense you don't want to take lightly, especially if you have a large deployment requiring several large UPS. If you rent space in a hosting data center that provides its own battery backup, how long the UPS can power the system before complete failure. Also, ask about previous power failure occurrences and durations (see Chapter 2 to learn more about data center power and how to assess hosting facilities). If you're not comfortable with the answers, by all means insure installing your own UPSs in addition to the data center's battery backup (or choose another provider).

# Using Generators for Emergency Power Supply

Generators can produce electricity to replace a failed power supply for long periods of time, as a result, generators can be indispensable during power outages. Most generators are powered by gasoline or turbine engines, as you learn in later sections. These systems are expensive, and they require monitoring, upkeep, and maintenance to ensure that they'll be ready to step into action when necessary. In addition, they require a UPS to properly condition the power before it reaches your systems, in order to avoid spikes and other aberrations that can harm electronic equipment.

If you rent space in a collocation facility, you probably don't have to worry about supplying (or maintaining) generator backup for your equipment. Most large data centers have their generators to power their own and customers' systems throughout power loss. Nevertheless, don't assume that your provider's system meets your needs; ask these questions:

- At what point during a outage are generators brought online?
- Do you notify customers when a power outage occurs?
- How long can the generators run on one tank of fuel?
- Who provides the fuel and how often are the generators refueled?
- How often are the generators tested? Is there risk to your equipment during these tests?
- Is the transition from wall power to generator power smooth, or is there a short outage during the switchover? Do you have UPS backup to cover this outage?
- How is the decision to make switch back to utility power?
