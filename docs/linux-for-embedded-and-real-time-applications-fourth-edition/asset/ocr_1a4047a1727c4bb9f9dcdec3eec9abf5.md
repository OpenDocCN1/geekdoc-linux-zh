# 4  Chapter 1

give is the engine control computer in your car. You don't drive the car any differently because the engine happens to be controlled by a computer. Oh, and there's a computer that controls the antilock brakes, another to decide when to deploy the airbags, and any number of additional computers that keep you entertained and informed as you sit in the morning's bumper-to-bumper traffic.

I go on to point out that there are a lot more embedded computers out in the world than there are PCs. In fact, recent market data shows that PCs account for only about 2% of the microprocessor chips sold every year. The average house contains at least a couple dozen computers, even if it does not have a PC.

Is an Android smartphone an embedded system? It is small, self-contained, and has limited input/output capabilities. Nevertheless, you can personalize it and download “apps” to your heart’s content. In that sense, it’s really more of a general purpose computing appliance. So I would say no, an Android phone is not an embedded system.

From the viewpoint of programming, embedded systems show a number of significant differences from conventional “desktop” applications. For example, most desktop applications deal with a fairly predictable set of I/O devices—a disk, graphic display, a keyboard, mouse, sound card, and network interface. And these devices are generally well supported by the operating system. The application programmer doesn't need to pay much attention to them.

Embedded systems, on the other hand, often incorporate a much wider variety of input/ output I/O) devices than typical desktop computers. A typical system may include user I/O in the form of switches, pushbuttons, and various types of displays often augmented with touchscreens. It may have one or more communication channels, either asynchronous serial, USB, and/or network ports. It may implement data acquisition and control in the form of analog-to-digital (A/D) and digital-to-analog (D/A) converters. These devices seldom have the kind of operating system support that application programmers are accustomed to. Therefore, the embedded systems programmer often has to deal directly with the hardware.

Embedded devices are often severely resource-constrained. Whereas a typical PC now has eight or more GB of RAM, and maybe a terabyte of disk, embedded devices often get by with a few MB of RAM and nonvolatile storage. This too requires creativity on the part of the programmer.

# What is Real-Time?

Real-time is even harder to explain. The basic idea behind real-time is that we expect the computer to respond to its environment in time. But what does “in time” mean? Many