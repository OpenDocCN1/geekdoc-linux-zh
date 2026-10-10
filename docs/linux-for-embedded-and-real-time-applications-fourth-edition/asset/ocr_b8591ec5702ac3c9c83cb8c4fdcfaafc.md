![](bbox=[0.71, 0.1, 0.87, 0.13])

# # The embedded and real-time space

+   - Chapter Outline
+   - What is Embedded? 3
+   - What is Real-Time? 4
+   - How and Why Does Linux fit in? 5
+   	- Open Source 6
+   	- Portable and Scalable 7
+   - Where is Linux Embedded? 8
+   - Open Source Licensing 9
+   	- Legal Issues 11
+   - Alternatives to Linux 11
+   	- FreeRTOS 12
+   	- MicroC/OS 13
+   - Resources 14

> > If you want to travel around the world and be invited to speak at a lot of different places, just write a Unix operating system.
> > — Linus Torvalds

# ## What is Embedded?

When I wrote the first edition of this book back in 2002, the notion of embedded computing devices was not widely appreciated. Back then many homes had at least a VCR and/or a DVD player and maybe a Tivo, all of which have at least one embedded processor. Most other appliances of the era were still basically electromechanical.

These days, virtually every appliance has an embedded computer in it. People are much more used to digital user interfaces, and while they may still not fully appreciate the nature of embedded computing, they are at least vaguely aware that they are surrounded by computers 24/7.

When I have to explain what I do for a living, I usually start by saying that an embedded system is a device that has a computer inside it, but the user of the device doesn’t necessarily know, or care, that the computer is there. It is hidden. The example I usually