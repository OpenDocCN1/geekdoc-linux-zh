
## 21.6 Different types of browse server

Up to now we’ve concentrated on browsing as seen by the client. We now have to look at two issues concerning browse servers:

1. How does a machine decide whether to become a browse server? How does a browse server decide whether it ought to act as a segment master browser, or even the domain master browser?
2. All the browse operations we’ve seen depend on broadcasting to announce a PC’s presence on the segment and to find a browse server. How can this be extended to a LAN that contains routers, where broadcasts are limited to the local segment?

To answer these questions we must first look at the different types of browse servers you can have.

### Types of browse server

A PC can play four (or five) different server roles in the browsing system:

1. **Segment master browser**: there can be only one of these per network segment. It listens on a segment for announcements (from machines in its domain only) and from those announcements builds up the browse list for the local segment. It can also service `GetBackupList` and `NetServerEnum2` get-browse-list requests from clients on this segment.
2. **Backup browsers**: these don’t accumulate the browse list themselves. (In fact, they can’t: announcements are made to `domainname<1d>`, which is a unique NetBIOS name that only the segMB has registered, so only the segMB can hear the announcements.) Instead, every 15 minutes or so they retrieve a copy of the current browse list from the segment master browser. However, backup browsers can and do service get-browse-list requests from clients on this segment. This improves the performance of the system, which is one function of backup browsers. Their other function is to be able to take over from the segment master browser if it fails.
3. **Potential browsers**: these aren’t acting as browse servers at all, but if the segment master browser or some of the backup browsers fail, they may become browse servers if necessary. Most Windows PCs are potential browsers. In the next module we’ll see how potential browsers can change state and become backup or master browsers.
4. **Domain master browser**: there can be only one of these per domain, irrespective of how many network segments there are. It communicates periodically with each of the segment master browsers on each of the network segments and retrieves their segment-specific browse lists. It merges these into a single browse list covering the whole domain, which it sends back to each segment master browser. In this way, every segment can get a complete browse list for the whole network.

The PDC always acts as the domain master browser. The domain master browser registers the NetBIOS unique name `domainname<1b>` (which, incidentally, is often used to find the PDC, even though strictly it’s only the domain master browser).

5. **Non-browsers**: this never, ever becomes a browse server.

There is no NetBIOS group name to identify backup browsers on this segment – you can only find out which they are by asking the segMB for a list of them. All potential browsers do register `<1e>` as explained in the next module. However, if you ask WINS to resolve `<1e>`, it gives you 255.255.255.255 to force you to broadcast to the group name as usual. (The Samba `nmlookup` tool is great for exploring this type of issue – you can issue specific queries and explicitly see the results.)

### Replication from master to backup servers

We haven’t explained yet how a machine decides which role it’s to fulfill, but for now, let’s assume we have a browse master and a population of backup browsers, and see how they interact. The mechanism is very simple:

- Every 12 minutes, each backup browser contacts the segment master browser (they locate it by broadcasting to `domainname<1d>`).
- Using `NetServerEnum`, the backup browser asks the segMB for:
  - a. The latest browse list of servers in this domain.
  - b. The latest list of domain names.
- The segMB replies with the lists. The reply isn’t just a set of changes or updates since last time; the list is returned in its entirety every time.

Figure 21.8 shows a backup browser, 212.140.133.35, regularly contacting the segMB, 212.140.133.13, and on each iteration requesting the two lists. (The “T” field is time since the packet on the preceding line.)

![](img/a2132b646d336d5f9a21102d6320e537_596_0.png)

In the next module we’ll see how a machine decides which role it is to fulfill.

## 21.7 Deciding which PC takes on which role; elections

There are Windows Registry settings (see Notes) to make a PC a non-browser, or to make it a preferred master browser (i.e. it wants to be either the master browser or at least a backup browser). Unless it’s a non-browser, it’s automatically a potential browser, at least. In this module we explain what happens when a potential browser PC starts up, and in the next module we show a line-by-line trace.

When our PC starts:

1. It announces its presence to `domainname<1d>` – as every machine does.
2. Because it may become a browser later on, it registers as part of the NetBIOS group `domainname<1e>`, which is the *browser election group*.
3. It broadcasts a `RequestAnnouncement` browser request to `domainname<1d>`. This asks the segMB (for `domainname`, on the local segment) to announce itself, which is how our PC finds the segment browse master.

What happens next depends on whether our PC got a reply in step 3. Let’s assume there’s no reply (e.g. we’re just building our network and this is the first machine to be added, or the segment browse master is down):

4. Our PC forces a *browser election* in order to nominate a new segment browse master. It does this by sending a `Browser Election (Force)` request, broadcasting it to `domainname<1e>` which is heard only by browsers and potential browsers (see step 2 above).

`domainname<1e>` is treated specially by WINS (if you are running it). When a PC asks WINS to resolve `domainname<1e>`, WINS returns the IP address 255.255.255.255, so the PC then broadcasts to this address whatever it was going to send to `<1e>`. This ensures the election stays local to the sub-net, which is what we want. Remember, it is the *segment master browser* that we’re electing.

5. Each browser and potential browser, including our PC, joins in the election by replying with an `Election` packet containing details of this machine’s operating system and current browser role, coded as a 4-byte number called its *election criteria*.

The election criteria are encoded so that Windows NT Server machines have priority over other operating systems, then NT Workstation, then Windows-9x, so that server machines are most likely to win the election. For machines with the same operating system, priority is given to the PDC, then a preferred master browser, then an existing master browser, and finally a backup browser. Figure 21.9 shows the election criteria values for an NT 4.0 server currently acting as both segMB and domMB.

6. Every machine participating in the election compares its own election criteria with the criteria in all the `Elections` received from other machines. The one with the highest value of the criteria wins, becomes the segment browse master, sends a few more `Elections` just to make sure that everyone has heard, registers itself as `domainname<1d>` (segMB), and finally announces itself as the segment browse master. If things are working correctly, there will be no responses to these `Elections` because all the other machines realize this machine has the best criteria.

```text
BROWSER:  Command   =  Election  [0x08]
BROWSER:  Election Version  =  1  [0x1]
➔BROWSER:  Election Criteria  =  536944042  (0x20010FAE)
➔BROWSER:  Election OS Summary  =  32  (0x20)
      BROWSER:  ...0  =  Not WFW
      BROWSER:  ...0.  =  Not used
      BROWSER:  ...0..  =  Not used
      BROWSER:  ...0...  =  Not used
      BROWSER:  ...0....  =  Not Windows NT Workstation
      BROWSER:  ..1.....  =  Windows NT Server
      BROWSER:  .0......  =  Not used
      BROWSER:  0.......  =  Not used
BROWSER:  Election Revision  =  271  (0x10F)
➔BROWSER:  Election Desire Summary  =  174  (0xAE)
      BROWSER:  ......0  =  Not Backup Browse Server
      BROWSER:  ......1.  =  Standby Browse Server
      BROWSER:  ......1.  =  Currently Master Browse Server
      BROWSER:  .....1..  =  Domain Master Browse Server
      BROWSER:  ....0...  =  Not used
      BROWSER:  ...1....  =  Transport Running WINS Client
      BROWSER:  .0......  =  Not used
      BROWSER:  1.......  =  Windows NT Advanced Server
BROWSER:  Server Up Time [DD:hh:mm:ss]  3:20:47:56
BROWSER:  Election Server Name  =  HAL9000-NT
```

**Figure 21.9** Network Monitor trace: **Election** criteria values

In fact, what we’ve just described is an over-simplification:

- To reduce the amount of network traffic, in step 5 machines delay a certain amount of time before sending their `Election` details. The current browse master replies to the `Election (Force)` after 1/10 of a second; backup browsers delay randomly for 2/10–6/10 of a second and others delay for 8/10–3 seconds.
- While waiting to send its own `Election`, if a PC hears one from another machine that indicates the other PC would be elected, this PC doesn’t bother sending its own `Election`, because it knows it’s going to lose the election and sending its own `Election` would only waste network bandwidth and processing power on other machines.

These two features mean that the existing segMB will broadcast first, and unless a better candidate has just joined the network, the existing segMB will win the election immediately, so there will be very little election traffic in practice.

The above describes the case where our PC got no reply to its `Request Announcement` in step 3. If our PC does hear the segMB reply with an `Announcement`, our PC compares the segMB’s criteria (which are included in the `Announcement`) against its own criteria; if our PC’s criteria are worse, there’s no point forcing an election, so our PC just announces itself as a potential browser and joins in the browsing system as normal.

Elections also occur (i) when a preferred master browser PC boots, (ii) when any PC boots and can’t find a segment master browser, (iii) when a backup browser tries to contact the master and it’s not available, and (iv) when a master browser closes down gracefully (because it forces an election as it goes).

In the next module we look at the trace of an election line by line.
