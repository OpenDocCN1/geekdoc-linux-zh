
# REVIEWED! NEW Pi 3 B+

www.linuxuser.co.uk

# LinuxUser

THE ESSENTIAL MAGAZINE FOR THE GNU GENERATION

# & Developer

# ELECTRONICS

# FOR

# PI HACKERS

- Go beyond kits
- Design circuits
- Build boards

OPEN SOURCE SAVES LIVES

# NEXT-GEN DISTROS

3D-printing critical medical supplies

Discover the future of Linux

IMPROVE YOUR CODING!

# 43 PAGES OF GUIDES

MYCROFT MARK II

- Speed up Python with JIT compilers
- Write safe and secure code with Ada
- Stream to Twitch with Raspberry Pi

# Open voice assistant for everyone

# LINUX ON DELL

Latest on Project Sputnik + New XPS

# Calculate Linux

The Windows replacement for your business

# Python shells

Boost your productivity with the best interactive shells for Python

# ALSO INSIDE

- Kernel in-depth
- Turn Make into a sync utility

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_1_0.png)

The Electronic Frontier Foundation is the leading nonprofit organization defending civil liberties in the digital world. Founded in 1990, EFF champions user privacy, free expression, and innovation through impact litigation, policy analysis, grassroots activism, and technology development. We work to ensure that rights and freedoms are enhanced and protected as our use of technology grows.

# EFF.ORG

# ELECTRONIC FRONTIER FOUNDATION

Protecting Rights and Promoting Freedom on the Electronic Frontier

# LinuxUser & Developer

# Welcome

to issue 19 of Linux User & Developer

# in this issue

- » Electronics for Pi Hackers, p18
- » Next-gen Distros, p64
- » Reviewed: Raspberry Pi B+, b86

Welcome to the UK and North America's favourite Linux and FOSS magazine. We look back at what dismay us this past month as we reflect on the passing of Professor Stephen Hawking, a giant in the field of theoretical physics and most 'intelligent' guest on The Starship. We also had the Pi-shaped appearance on our radar (see p86 for Raspberry Pi B+), which we cleared out to be of new Pi, so we've consoled concerns with a big, Electronics for Pi Hackers (p18) building circuits and ways to invent the Pis with the new Linux 3 B+ is a great addition with inspiring networking charms, and we've already predicted for futures in issue. Also this month, we attempt to predict what the big trends will be in Linux distros (p64); look at the new XPS 12 (p62) and consider the fantastic world of Google Sputnik, using medical devices (p32). Of course, to top all off we have a hearty batch of tutorials to deavour! Enjoy Chris Horner,

Future PLC Quay House, The Amery, Bath BA1 9UA

Editor Chris Thornton
chris.thorne@linuxuser.com
0179 6814
Designer Rosie Webber
Producer Ed J. Ricketts
Editor in Chief, Tech Graham Barlow

Senior Editor Jo Guiller

Michael Aucloss, David Bedford, Adam Miles, Mike Reed, James, Thomas Courtney, Nicholas Taylor, John Jones, Tom Castillo, Martin Price, Patrick O'Neill, Anthony Page, Paul Smith

All copyrights and trademarks are recognized and respected. Linux is the registered trademark of LinuxUser in this issue and other countries.

Advertising
Media space is available on request.
dave@dortuser.com
clare@dortuser.com

Subscriptions
For information about subscriptions contact
richard.hemming@futurenet.com

Account Andrew Treeby
Account Manager Richard Cripton
richard.hemming@futurenet.com
020125 68735

Linux User is available for licensing. Contact the
International Department to discuss opportunities.
International Licensing Director Matt Ellis
matt@linuxuser.com

Subscriptions
Email us at contact@mysfutureuser.com
UK orders: 01638 648 663
Outside the UK call +44 016 648 0442
Online orders & enquiries: manage@linuxuser.com

Circulation
Head of Heatrix Masters

Production
Head of US & UK Westmarket
Production Manager Claire Scott
Graphic Designer James
Digital Content Creator James Hobson Booth

Management
Account Manager Aaron Aarsi
Editorial Director Paul Newman
Marketing Manager David King
Head of Art & Design Robin
Director Jan Johnston

Printed
By Vanderbilt Publishing, Storey's Road,
Peterborough, Cambridge, PE1 9SG

Marketofke, 5 Circus Place, Canary End, London, E3 4NH
www.marketofke.com
020 7412 2000

We are not responsible for any opinions expressed by users who have submitted articles published in this magazine. The views, opinions, strategies, or policies expressed in any article do not necessarily reflect those of LinuxUser or Future Media Ltd.

NEW LETTERS PRIZE
Write to us and win an istodash! Pro!
luxuser@futurenet.com
Twitter: @LinuxUsermag
Facebook: facebook.com/LinuxUserUK
FIND MORE DETAILS ON PAGE 11

For the best subscription deal: visit myfutureuser.co.uk/subscribe/Save up to 20% on print subs! See page 30 for details

Linux User is available in print and online.
Future plc, London Street
London, EC2 4NQ
www.futureplc.com

FUTURE
Creating
Digital Media

Chief executive Ethan Smyth-Thorne
Chief financial officer Paul Ledham
Tel: 020 7936 000

www.linuxuser.co.uk | 3

# Contents

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_3_0.png)

# 18
COVER FEATURE

# ELECTRONICS
FOR
# PI HACKERS

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_3_1.png)

# 58
THE FUTURE OF
# PROJECT
# SPUTNIK

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_3_2.png)

# 64
NEXT-GEN
# DISTROS

# OpenSource
# Features
# Tutorials

- 06 News
Is Canonical collecting user data?

- 18 Electronics for Pi Hackers
Interface to your Raspberry Pi by building published circuits on breadboard, or designing your own circuits for construction on a project budget. Make Bestford shows you how to get started

- 38 Essential Linux: GNU Make
Use GNU Make for different purposes than building projects

- 10 Letters
You let us know what's what

- 42 Anible
Get started with the tool that enables you to update software remotely

- 12 Interview
We-chat with Mycroft about its follow-up to the first open source personal assistant with voice control

- 58 The Future of Project Sputnik
Dell's Project Sputnik - an initiative to offer its flagship PCs with Linux out of the box, fully supported - has gone from strength to strength. How does it work within the company, and what's on the horizon?

- 44 Security: MITM attacks
Learn how-man-in-the-middle attacks work, and how to defend against them

- 16 Kernel Columm
Jon Masters on the latest happenings

- 48 Python: PyPy Numpy
Speed up your programs using these JIT compilers

# InspireOS

- 52 Programming: Data
An introduction to the venerable language that boasts extremely strong static typing, among other things

- 32 Open source medical
The project is saving lives in Gaza with cheap medical equipment

- 64 Next-gen Distros
Which distributions will be used in the years to come? Paul O'Brien investigates – and wonders the growth of alternative approaches to Linux mean the OS could feel very different in the future

# LinuxUser & Developer
Issue 190
April 2018
facebook.com/LinuxUser
Twitter: @linuxusermag

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_0.png)

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_1.png)

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_2.png)

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_3.png)

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_4.png)

# Practical Pi

# Back page

- 72 Pi Project
Designer and creative technologist Peter Buczkowski explains his Photographer project – a camera that visually shocks you into taking a picture when it demeans a scene is good!

- 62 Dell XPS 13 9370
Does Dell's latest update deliver?

- 81 Group test: Python shells
We put four alternatives to the standard interactive shell to the test

- 74 Access a Raspberry Pi Zero using a laptop
It's easy to configure OS settings and use the port to access both the command line and GUI from another computer–we show you how

- 86 Raspberry Pi 3 B+
Not the P4, a worthy addition

- 88 Calculate Linux 17.12.2
Based on Gentoo, desktop-oriented distros claim to make it more approachable, but does it?

- 76 Stream to Twitch with a Pi
Discover how to turn a Pi into a dedicated streaming device, and interface with platforms such as Twitch to broadcast your streams

- 90 Fresh FOSS
LimeSource 3.4.1, uBlock Origin 1.15.10, Zeal 0.6.0 and Rapid Hot Downloader 0.9.8– reviewed

- 96 Top open source projects
What projects are ticking developers' fancies this?

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_5.png)

# SUBSCRIBE TODAY
Save up to 20% when you subscribe! Turn to page 30 for more information

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_4_6.png)

www.linuxuser.com | 5
