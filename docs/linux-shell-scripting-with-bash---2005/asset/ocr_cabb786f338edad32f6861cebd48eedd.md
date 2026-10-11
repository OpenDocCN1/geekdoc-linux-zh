# 10

Job Control and Signals

Although I grew up on a grape farm, I didn't spend a lot of time out in the fields. I suppose that was my father's way of not biasing me towards a life of sweat and sunburns. Somehow one farming skill that I never mastered was the use of hand signals. It seemed like those who had spent years outdoors were used to gestulating over distances and noise, able to understand the most incomprehensible motioning. Not so for me.

One summer my father was trying to place a heavy piece of equipment into the back of a pickup truck using his tractor. He had me stationed at the base of the truck to line up the equipment and tell him when to start lowering. When everything looked in position, I gave him the signal. Unfortunately, my glasses are thick enough that they cause spherical aberration—that is, things sometimes appear crooked because the light passing through the lenses is bent. Almost at once I saw that the equipment wasn't centered and I started hopping up and down, gesturing wildly. But my father didn't notice anything was wrong until the equipment caved in the side of the truck with a sickening crunch.

Whether it was my bad signaling or his failure to pay attention is beside the point. An important condition had risen that was unable to be communicated. Similarly, scripts need to be able to delegate responsibilities to other scripts and to interrupt each other when pressing matters arise. This cooperation is achieved through job control and Linux signal handling.

# Job Control

You can start background tasks by typing an ampersand (&) at the end of a command. Bash refers to background tasks as *jobs*. Any command or script running in the background is a *job*. During an interactive session, the shell keeps a list of all outstanding jobs. Managing background tasks using Bash commands is called *job control*.

Job control is available by default at the command prompt but must be enabled in scripts with the `-o monitor` shell option. Without job control, background tasks can still be started from a script, but Bash's job-management commands are unavailable.