
## Goals

The first thing to consider when planning your network (and where your router(s) fit into that plan) is your overall goals for your network.

Are you just devising a small home LAN that's going to serve for two or three computers sharing a dial-up connection, DSL, or cable modem? Or is this going to be a WAN joining LANs in three different states and providing a VPN for your company's various remote offices and road warriors dialing up from their hotel rooms to check email and transmit sales figures?

As you can see, the answers to these questions will start to shape your planning and dictate the type of protocols you'll need to support as well as the hardware that will be needed to support it. (It will also determine which chapters you'll need to read thoroughly and which ones, if any, you can skim!)

## Resources

The next question is: What resources do you have to fall back on? This will provide a clear picture of what you have to work with while trying to achieve your goals and how aggressive you can be in terms of future-proofing your setup and providing redundancy.

For instance, can you afford to deploy redundant systems? For corporate setups, we strongly recommend that you take the time to build a back-up system for each mission-critical system. This is particularly true if you have small remote offices without dedicated technical staff. Should you suffer a hardware failure, you can simply have someone swap out the dead or malfunctioning system with a backup and proactively reduce your downtime from hours or days to a few minutes. Almost anybody can be trained to swap out a standard system.

## A Word About Reliability

We're not trying to convey the message that Linux is unreliable. Quite the contrary...many folks have Linux systems with uptime measuring in years. That's right—years. However, you'll probably be building your system with standard PC components that have mechanical parts, and eventually those parts will fail. Note that we didn't say they might fail—they will fail. It's only a matter of when and how prepared you'll be when it does happen.

You can protect yourself somewhat by buying decent components, but even the cream of the crop can suffer unexpected failure. Even a Rolls Royce can get a flat tire.

Another question is whether you'll be buying new systems or if you're going to be digging through the company's computer "bone yard" to scrape together parts for your soon-to-be router. If your needs are small, there's quite a lot to be said for recycling old hardware and repurposing it with Linux. Actually, we rather like the fact that Linux allows you to reclaim hardware that might have otherwise gone to the junkyard.

Maybe your situation allows you to purchase one new system to build your router, but you can build a backup system from old parts to pinch-hit in the event the primary system fails.

## Budget Concerns

In an ideal situation, you have unlimited spending authority, don’t have to justify your hardware purchases, and your budget rivals Bill Gates’s yearly income. Of course, in an ideal situation you’re independently wealthy and building Linux routers just for the sheer joy of it.

More than likely you’ll have a fixed amount of money to spend on your routing project and a fixed amount of time as well. Don’t skimp on hardware or time spent up front, only to have to spend more money later on, or even worse, more time fixing bugs or issues that could have been solved up front.

## Growth

Is your network going to be growing (or shrinking!) in the foreseeable future? If you can reasonably expect that your network is going to undergo significant growth in the next six months to a year, you might want to plan your router as if the growth had already occurred.

For instance, if you know your company plans to open its first remote office in a few months, now is the time to start planning for a WAN and budgeting for equipment for the remote office. Life will be much easier if you can set up and test equipment weeks or months in advance and just plug it in the day before employees start turning up at the new office.

## Dealing with ISPs and the Phone Company

It’s a nightmare to show up at a new office planning to get to work only to find out that the T1 that was supposed to be installed a week ago is going to take another month. Even worse is what happens when 20 employees try to share a dial-up connection to send and receive email and do work on a remote server.

This does happen, particularly when admins think they can have a T1 installed at a location as quickly as they can get residential phone service. Order your connectivity at least a month ahead of time and confirm the order at least a week before the turn-on date. Don’t schedule installation the same day that workers will be arriving and expecting to get to work, either. That’s a recipe for disaster.

If you’re reading this and shaking your head in disbelief that we feel it necessary to point these things out, you’re lucky. Some of us have worked with admins and CTOs who didn’t understand the importance of preplanning when dealing with phone companies—and lived to tell the tale.
