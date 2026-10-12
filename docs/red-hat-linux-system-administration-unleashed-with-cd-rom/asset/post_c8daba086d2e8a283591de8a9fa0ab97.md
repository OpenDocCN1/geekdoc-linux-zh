
## General Bottleneck Focal Point Location

Is it within the box? This is one of the most important questions to ask yourself and to determine quickly. Is it within the box or a network issue? It is also one of the most confusing when network file transfers, system-to-system database transactions, or multinode intranets come into play. Network issues can often cloud the perception of where a bottleneck may be. It may not even be on the system you are examining at all, or it may be on the network or another host altogether.

What other processes that do not appear to be intensive are running? As an example, let's say that when job X on Linux server Larry runs, there are normally only 100 users logged in. For some reason, on this particular day there are 200 users logged in. When you scanned the top monitor (mentioned later in this chapter), you didn't notice the other users or maybe it looked like they were not individually eating up resources. This can happen and you might be surprised if it does.

## Relative Importance of Tuning

Is it even worth it? The next section, "Weighing Costs and Benefits," discusses this in greater detail, but it also deserves mention in the "Considerations" context. Can the users live with it? Can you? Perhaps even more important, can the system?

Is there any risk involved? Number one question: Will you endanger the system by changing a kernel parameter or changing swap priority? Will an improvement here cause a detriment there? This is a very important, and tough, decision to make.

> **Note**
> 
> Always try to keep a "basher box" or test system lying around to see how a change may affect a live system. Even though the systems may be radically different, at least you get a "warm fuzzy" for what changes you might expect to see. Most of the time, changes on a test system do accurately reflect how they would affect a live system.

No system is ever running at peak efficiency out of the box, even if the person who installed it was very specific about what the system would be doing, what services it would be running, and its general configuration. Chances are there is something, somewhere, that could be better or (as is more often the case) just isn't needed.

> **Note**
> 
> Unrequired services rarely put a load on a Linux system; however, some of them can actually cause a system to become somewhat unstable.

Unrequired services should be a no-brainer. Always look for unrequired services that were started or installed that you don't need. Aside from the obvious possible load they may put on the system, running unused (and subsequently unmonitored) services is a security risk. Coupled with the security issues is another very important issue: startup and/or recovery time. In a multiuser environment (in my own case, nearly 500 users at peak times) startup and recovery time is crucial. Unrequired services should be eliminated for the sole purpose of speed at boot time. A prime example of this is the Apache Web Server. Many distributions have Apache turned on by default; however, what if you never plan to use it? It is wasting processor cycles regardless of how lightweight the Apache processes may be. This also relates to the troubles of micro-examining a system and changing configurations, as discussed in the following section.

## Weighing Costs and Benefits

There is a wide variety of different costs with a common benefit—better performance. The costs come in the form of money and time. They include money required for more hardware, the time (which ends up costing money) a system must be down, or the time in man-hours required to increase a system's level of performance.

Many performance issues (especially memory-related ones) can only be solved by purchasing newer or additional hardware. Granted, this is often the case with Linux systems and more so with other operating systems, but it certainly does happen. Sometimes the question arises as to whether it is worth the expense. Not only does the hardware cost issue arise, but man-hours are also a pertinent cost. Is it really worth the headache to spend hours, days, or sometimes weeks to find a better solution? Is it worth the cost in your or your department's man-hours? Piled on top of both of these is the ultimate cost-weighted (and most loaded) question: Is the whole system a bottleneck? Is it time for more than just more memory or more cache?

Ultimately, the question is when do you have to buy hardware and when can you get away with not buying it? The best way to answer this is through an example. One time that more hardware must be bought is when meeting minimum specifications. To install a certain database product, you may have to have a minimum of 512MB of memory and 1GB of swap space. Sometimes to scale that appropriately you may have to have a TB of memory and swap, whatever the case may be. If you do not have the required amount, chances are you will need it or you face a potentially crippling bottleneck. In other cases, a tape drive may not be finishing backups on time or requires multiple tapes, which then makes the backup run too long and slows down the system. You will most likely have to find a faster and higher density device.

## Hardware Costs

Hardware costs can become a complicated matter. At what point does it become prohibitive to continue to add hardware to a particular architecture? On RISC-based systems, this is usually a very easy question (consult the hardware documentation guides) but on x86-based systems, this can be very hard to determine. The reason for this is the incredible scalability of Linux systems. Many times, you can increase performance on other cost-versus-benefit weights such as using a less resource-intensive Window Manager (or not using one at all). In such a case, the loss is Window Manager eye candy and the gain is out-and-out performance. Another cost might be the time it takes to perform a full backup of data and repartition the system for better disk I/O performance. It does, however, often come down to more or newer hardware. There is a point that can be reached where the system is the bottleneck—you have reached the limit of upgradability and simply have to purchase a new system (again, a rarity in Linux).

> **Note**
> 
> One practice a systems administrator may find useful is "musical servers." How this works is relatively simple. Say you have three Linux systems, Larry, Curly, and Moe. Larry is the Web and FTP server. Curly is the mSQL database and Moe is your basher box. You buy a new server because Larry is under stress and you have used up its hardware scalability. But, it is more powerful than Curly, which is more powerful than Moe. Simply transfer Larry to the new system, and then Curly to Larry and now you either have two basher boxes or Moe has been freed up for some other purpose (your personal workstation?).

## System Requirements and Needs

Combining all of the elements of symptoms and cost ultimately leads to the big question, which is how much of a real need is this? Sometimes you will discover that the need is exaggerated or not as important as you were led (or led yourself) to believe.

Perhaps one of the biggest costs may be running the risk of damaging the system or facing major downtime to make enhancements. This cost issue is rare in Linux but can happen. You must also take into account when you are not sure what (if any) side effects will result in a change in how the system operates. Being prepared for a disaster is very important when deciding to make system-level changes. Sometimes things can (and seem more often to) go awry. This should be the number one factor when approaching critical problems such as filesystem and memory/cache issues. The cost may be more than you bargained for. Where this really comes into play is modifying the kernel and system parameters for better performance. Sometimes side effects may happen, and they may be worth it. Some processes within an organization do (and should) take priority over others and, as a result, you may be forced to cause some detriment to others to gain better performance for a given service or process. An example of this might be weighing the priority of a real-time process that collects data versus someone simply viewing files leisurely. The real-time data collection would be a higher priority. The key here is to ensure that you do not accidentally inflict system-wide detriment by "enhancing" a particular aspect of the system. Although this is rare, it most certainly can happen.

## Note

As will be noted in later chapters, always keep a backup kernel and snapshot of the system handy in case you are making critical changes to enhance performance.

## Performance Enhancements

Luckily, most performance enhancements do not require running the risk of blasting the system into oblivion. Shutting down unrequired services means that if someone was actually using one, it can be restarted. Many caching parameters can be enlarged or shrunken without affecting the system’s overall operation. It is important to note, however, what you are changing and how to undo it.

All of these factors must come into play when deciding on how to best serve the system’s performance needs. The system’s performance is ranked nearly beside stability and uptime. What good is a system if it is so slow no one is getting anything done? Not much, but with practice and patience, a system that appears to be slow can be tuned for optimum performance, which leads to how you determine where a problem is and how to tackle it.
