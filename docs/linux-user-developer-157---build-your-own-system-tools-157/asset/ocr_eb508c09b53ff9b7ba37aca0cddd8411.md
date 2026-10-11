# COMMENT

# Your letters

Questions and opinions about the mag, Linux and open source

![](bbox=[0.0, 0.3, 0.75, 0.59])

**Notes** Microsoft's settings ensure your private conversations are safely unrecorded until you use the keyword **Notes** The device can also control appliances like coffee machines and thermostats, and hook in to IFTTT

# Hackable butler

Hello Linux User & Developer, I've enjoyed reading Joey Bernard's recent articles about programming a JARVIS-like system for home automation with the Raspberry Pi. I did have a go at putting something together myself, which was very fun, but obviously quite a simple implementation. However, the idea of the project has really grown on me and I would now like to implement a more complete system. My question is this: can you recommend a system combining both open source software and hardware that I can then play around with and extend myself, to better fit the devices and needs I have at home?

Joe R

Hello Joe, We're really glad that you enjoyed Joey's tutorials! In terms of a more complete system for home automation, your choice is limited at the moment. Amazon Echo is probably the closest to what you are after in terms of the system and functionality, though it is proprietary and so not open to hacking and extension.

One project that we've stumbled across recently is Mycroft. It's another Kickstarter (kok.st/1hV2fNf) and at the time of writing it has just cleared its funding target with fifty hours to go ($107k/$99k), so the backers' units should ship out in July 2016 - this should fit your needs pretty perfectly. The Mycroft is a voice-controlled unit, inputting and outputting natural language, that can hook into online services and also interact with a selection of IoT and media devices. Mycroft can set alarms, send tweets, tell you the weather and read your calendar appointments. You can use regular expressions to perform specific shell commands. It can play music and videos, control devices like coffee makers, thermostats and wireless locks, or even connect to local Mycroft units for voice chat between rooms or house-wide announcements. The crucial part is not just the implementation on the software side and the reliability of the natural language input, but the sources that Mycroft can interact with. Media can be sourced from Netflix, Spotify, Pandora, YouTube, Plex and NPR. It can also be outputted to Chromecast and Roku devices. It can control WeMo, Philips Hue and Nest gadgets, plus SmartThings and Iris Smart hubs. In addition, it acts as both a source and a destination for IFTTT. It's a very solid start. In terms of openness, it is based on the Raspberry Pi 2 and an Arduino-compatible microcontroller with Snappy Ubuntu Core and open APIs powering everything. The team promises to produce comprehensive documentation on all the hardware and software, too. Since there's a Pi inside this open system, you'll be able to customise your Mycroft and share your own mods. It's an interesting project and worth keeping an eye on: mycroft.ai.