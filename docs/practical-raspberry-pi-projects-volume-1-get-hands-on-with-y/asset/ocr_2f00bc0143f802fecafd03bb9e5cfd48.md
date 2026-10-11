![](bbox=[0.12, 0.01, 0.8, 0.26])

# Raspberry Pi Car Computer

# RetroNES

Now you're playing with power. Raspberry Pi power to be exact, situated inside an old game console

Left: It's difficult to see, but there are some difference to this NES compared to an original.

+   **Maker Profile**
+   **Chris Crowder**
+   Programmer and database administrator
+   
+   Working in the car industry, Chris develops manufacturing systems for production floor systems using .Net and SQL. In his down time, he likes to play video games and tabletop games, but was previously limited to his PC for the former.
+   
+   Find out more: imgur.com/a/KPizn7/gallery

> “It was a little intimidating at first as I wanted to make sure that this project looked and felt like an NES”

“It all started when my wife asked me what I wanted for Christmas”, said Chris over email. “I had absolutely no idea but I had been wanting to mess around with a Raspberry Pi since it came out, so she got me a starter kit.”

“While waiting for Christmas I started narrowing down ideas and found the RetroPi project. I thought that I would just install that, load some ROMs and call it good, then I remembered that I had some old NES and SNES controllers in storage. I went to get them and found my old childhood NES console along with the controllers. Once I got the NES back in the house and started looking at it, I found that almost all of the internals were damaged due to insects and moisture. All of the connectors were corroded and some of the boards had traces that were peeling. That is when I decided that I would use the Raspberry Pi to “resurrect” the NES.”

Chris completely gutted the case and replaced the insides with a Raspberry Pi, hooking up I/O ports to the original connectors for the controllers and the AV cables and such. What’s it like taking on a project with one of the most revered consoles in videogame history?

“It was a little intimidating at first as I wanted to make sure that this project looked and felt like an NES but with more flexibility. The biggest issue I ran into was that I wanted it to be able to work like an NES, meaning that if someone wants to play a game that they just turn it on, select a game and then they are playing. When they are finished all they have to do is press the power button to turn the console off. We can’t do that easily with a Raspberry Pi since there is no ATX-style power switch. I was able to solve this issue with a Mauserberry Circuit and a Python script. When the power button is pressed it communicates with the Pi via a GPIO connection and it runs the shutdown command. Once the Pi is shut down, the circuit cuts the power to the Pi.”

The final product works great, with Chris reporting the can play on Atari, Sega and Nintendo games just fine. He’s now looking to upgrade it with a Raspberry Pi 2 and increase the number of games he can play.

![](bbox=[0.12, 0.75, 0.36, 0.91])

Above: Everything is packed inside the original case, without needing to open it up to use it.

+   **Refitting a NES**
+   
+   Do you fancy taking on the challenge of bringing your old console back to gloriously pixelated life? Thought so. In that case, you’ll be needing this – here’s a list of the equipment that Chris used to repair and revive his childhood NES console:
+   * A broken NES console – please don’t do this to a working console
+   * Replacement NES Door
+   * Canakit Starter B+ – soon to be replaced with a Raspberry Pi 2
+   * Panel Mount Ethernet Cable
+   * Panel Mount HDMI Cable
+   * Panel Mount USB Cable
+   * USB-A Male to Micro USB
+   * SNES USB Controllers
+   * Anker 13000 mAh 3 watt Battery – this is for when there is no power outlet nearby or you want to be portable
+   * Mauserberry Circuit – shutdown circuit that uses your own switch, USB
+   * LED-0 – to hold the Mauserberry Circuit
+   * Gorilla Glue
+   * Blue 3-volt LED – the original NES LED was 12 volts, plus all of the other items in Chris’ entertainment console are blue