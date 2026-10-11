# Feature

# Alarm Clock Robot

Chasing your alarm clock may sound like a
nightmare to some, but here it is in reality

![](bbox=[0.03, 0.11, 0.35, 0.38])

# Robotics
education

There are many ways to try and get kids
excited with coding. Like making games in
Scratch, modifying Minecraft and teaching
via robotics. The latter is a newer concept
but still has the same merits – a physical
creation that children are excited about then
react to the programming they’ve done on it.
Visible results and instant gratification is a
great way to get imagination fired up.

When we talked about Rolly the
alarm clock robot around the office,
most people burst forth with a string of
expletives not fit for print. It’s a stiflingly
evil invention – an alarm clock you need to work
for to turn off. It sounds like a great invention,
getting people who have trouble waking up to
actually get up out of bed and start the morning.

Like any other Dexter Industries robot, it runs
on BrickPi, the LEGO Mindstorms adapter for
the Raspberry Pi that enables it to interface with
LEGO kits via programming.

“Today almost everyone uses their phone as
an alarm clock, which has a range of benefits,”
the website explains. “Phones are easy to
set, easy to adjust, play custom songs and
can even sense when is the best time to wake
you up. The problem is, unless your phone is
across the room, we use our phones so much
we can literally use them in our sleep. Why not
build a robot that is able to do all these things,

# Maker Profile

# Taryn Sullivan

Advisor

Taryn is an international businesswoman. As well
as flying between Shanghai and DC for her own
engineering business, she now works with Dexter
Industries to promote robotics education.
Find out more: bit.ly/1BTrYxjv

but won’t stop till you get up and start moving!
Our robot will be able to easily move randomly
around the room over any surface, playing a
custom alarm tone.

In order to set the alarm, simply link the
program on the BrickPi to your Google account
and it will search events with the title “wake”
and automatically start the alarm at the event’s
time. This means the alarm time can very easily
be adjusted using any device that can access
your Google Calender.”

# PiFM Radio

Sometimes the simplest hacks can
open up whole worlds of possibility

# Maker Profile

# Oskar Weigl

Electronics
engineer

Oskar is an
electronics
professionals and
robotics as well as
an avid forward
and reverse
engineer.
Find out more:
bit.ly/1q86OE

When studying at Imperial College London,
Oskar Weigl and Oliver Mattos turned the Pi
into an FM radio by connecting a wire(antenna)
to GPIO 4 and using a custom Python module.

“There is a clock generation module in the
hardware of the Raspberry Pi chip that lets
you output a clock signal at a user-selected
frequency,” Oskar explains. “We used the DMA
controller to send commands to the clock
module to change the frequency and achieve
frequency modulation. We had to overclock the
clock generation module by a factor of 20 times.
The sound is 14 bits per sample, enhanced
to a higher number of bits using delta sigma
modulation and the range is at least 50 metres.”

# Ras Pi Smart TV

Is your smart TV not smart enough?
Open the case and put a Pi inside

# Maker Profile

# Tony Hoang

Graduate
researcher

Tony Hoang is a PhD
student studying
computational
biophysics and
single molecule
research at SUNY-
Albany in Albany.
Find out more:
linkedin.com/in/
tonyhoang

“There’s plenty of room for additional electronics
inside the Hisense LED smart TV,” begins Tony
Hoang. “There’s a large flat area for electronic parts
in the centre of the TV where I placed my Raspberry
Pi. The dual down-facing speakers were quite loud,
so I removed one and replaced it with a USB hub. The
back panel was mostly flat, so finding a spot for the
LAN port and HDMI output wasn’t too hard.

“The Raspberry Pi is powered by the logic board
of the Hisense. There were the obvious 5v/500 mA
outputs from the 2x USB 2.0 ports, which I tried but
I found out that the logic board shuts off the power
to these ports when the TV turns off. To keep the
Raspberry Pi turned on, I probed the logic board with
a multimeter and found one from an unused GPIO.”