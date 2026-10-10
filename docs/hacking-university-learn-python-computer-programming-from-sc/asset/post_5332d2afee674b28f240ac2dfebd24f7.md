
It is confusing to look at for the first time, but comments help to demystify the complex characters. Moreover, coming back to an old script of yours from weeks past can feel like reading a foreign language—comments help you to quickly get back to coding. Many programmers put a comment as the top line of their program with a brief description of what the script does, when it was written, and any contributors to it. That way the next time you are quickly looking through files trying to find a certain program, the comments can help you understand what is inside without actually running or deciphering the code.

The final common mistake that runs rampant in Python newbies is variable naming. If it has not already been brought to light in your experimentation, there are just certain names that you cannot name your variables. “Reserved ” words such as class, break, print, and, or, while, etc... are keywords that cannot be used for a variable name. If Python detects their use a syntax error will occur. Besides errors, though, programmers often use bad form when naming their variables. Avoid ambiguous and simple variable names such as “number” or “var1” in favor of descriptive one such as “user_input” or “totalNumberOfDogs”. These variables explain their use at a glance, so a verbose programmer will never misuse a variable or have to check what its intent is. Python programmers typically use the underscore method to name their variables (grade_average, dog_1), but camelCase is acceptable as well (userInput, multiAnswer). No matter which method is used, a skillful programmer will always make the name descriptive.

## Conclusion

Thank you again for downloading this beginner’s guide to Python. Now that you have finished the text, you have a basic knowledge of how Python works, and you should be able to write your own programs. You can further increase your knowledge by attempting to create larger and more complicated programs, or you can study modules and learn new functions. If you have enjoyed the book, rate and leave a review on Amazon so more high quality books can be produced.

# Hacking University Senior Edition

# Linux

Optimal beginner's guide to precisely learn and conquer the Linux operating system. A complete step-by-step guide in how the Linux command line works

*BY ISAAC D. CODY*

# HACKING UNIVERSITY

# SENIOR EDITION

# LINUX

Optimal Beginner's Guide To Precisely Learn And Conquer The Linux Operating System. A Complete Step By Step Guide In How Linux Command Line Works

![](img/fd3b07b76342e40d21bbab5fa5696daf_120_0.png)

# ISAAC D. CODY

# Table of Contents

- [Introduction](#)
- [History of Linux](#)
- [Benefits of Linux](#)
- [Linux Distributions](#)
- [Booting Into Linux](#)
- [Ubuntu Basics](#)
- [Installing Linux](#)
- [Managing Hardware and Software](#)
- [The Command Line / Terminal](#)
- [Managing Directories](#)
- [Apt](#)
- More Terminal Commands
- Connecting to Windows / Mac Computers
- Useful Applications
- Administration
- Security Protocols
- Scripting
- Advanced Terminal Concepts
- I/O Redirection
- More Linux Information
- What Next and Conclusion

# Copyright 2016 by Isaac D. Cody - All rights reserved.

This document is geared towards providing exact and reliable information in regards to the topic and issue covered. The publication is sold with the idea that the publisher is not required to render accounting, officially permitted, or otherwise, qualified services. If advice is necessary, legal or professional, a practiced individual in the profession should be ordered.

- From a Declaration of Principles which was accepted and approved equally by a Committee of the American Bar Association and a Committee of Publishers and Associations.

In no way is it legal to reproduce, duplicate, or transmit any part of this document in either electronic means or in printed format. Recording of this publication is strictly prohibited and any storage of this document is not allowed unless with written permission from the publisher. All rights reserved.

The information provided herein is stated to be truthful and consistent, in that any liability, in terms of inattention or otherwise, by any usage or abuse of any policies, processes, or directions contained within is the solitary and utter responsibility of the recipient reader. Under no circumstances will any legal responsibility or blame be held against the publisher for any reparation, damages, or monetary loss due to the information herein, either directly or indirectly.

Respective authors own all copyrights not held by the publisher.

The information herein is offered for informational purposes solely, and is universal as so. The presentation of the information is without contract or any type of guarantee assurance.

The trademarks that are used are without any consent, and the publication of the trademark is without permission or backing by the trademark owner. All trademarks and brands within this book are for clarifying purposes only and are the owned by the owners themselves, not affiliated with this document.

# Disclaimer

All rights reserved. No part of this publication may be reproduced, distributed, or transmitted in any form or by any means, including photocopying, recording, or other electronic or mechanical methods, without the prior written permission of the publisher, except in the case of brief quotations embodied in critical reviews and certain other noncommercial uses permitted by copyright law.

# Introduction

Computers contain two functional components—software and hardware. The hardware is the physical parts that spin, compute, and use electricity to perform calculations, but software is a more virtual concept. Essentially, software consists of programming code that gives instructions to the hardware—telling the parts what to do. There is “high level” software such as Internet browsers, word processors, music players, and more. But the often overlooked component is the “low level” software known as an operating system.

Operating systems are required for our personal computers to work. At an office, or with a relatively inexpensive desktop computer the operating system used is probably Microsoft’s Windows. Content creators, writers, and graphic artists prefer Apple computers because they come with the creativity-focused OSX operating system. Those two OS’s, Windows and OSX, have dominated the consumer market for many years. However, an alternative operating system exists that excels in usability, customization, security, and price. OS’s based off of the relatively unknown Linux meet and exceed in all of those areas, but it remains an obscure option that many people have not even heard of.

Linux is not an operating system by itself. It is a kernel, or the “core” of an OS. Just as Windows NT is the kernel of Windows 7, Linux is the kernel of “distributions” such as Ubuntu, Debian, Arch, Fedora, and more.

But why would anybody abandon the familiarity of Windows for an unheard of computing environment? Linux is not only monerarily free, but it is also compatible with a huge range of devices. Older computers, and especially ones that no longer work can be rejuvenated with a Linux OS, making it run as though it were new again.

This book will explicate upon the benefits of switching to Linux, as well as serve as a beginners guide to installing, configuring, and using the most popular distribution. Then, the terminal command line will be explained to tell how to take advantage of the OS in ways not possible in other systems. Truly there are many advantages to be gained by switching to Linux, and you just might find a suitable primary OS to use on your computers by reading this book.

# History of Linux

In the early 1990s Linus Torvalds was a student in Finland. Computers of the time usually ran on either DOS or UNIX, two operating systems that were both proprietary and difficult to use at the time. Torvalds sought to create his own operating system as a hobby project (based off of UNIX), but the project quickly grew and attracted more developers. The kernel continued to transform until it was portable (usable on a variety of systems) and entirely usable for computing. A kernel is not an OS, though, so Linux was combined with the GNU core utilities to create a computing environment reminiscent of an operating system.

Then, 3rd party organizations took the base Linux product and added their own high level software and features to it, thereby creating Linux “distributions”. Linux remains a free hobby project even through today, and thus the kernel is continuously receiving updates and revisions by Torvalds and the community. Throughout the 2000s, many other 3rd parties saw the usefulness of the Linux environment and they began to incorporate it into their production environments and corporations. Today, Linux is known for being highly used in servers and business settings with a small dedicated desktop following. Working towards the future, the kernel has reached a level of popularity where it will never die out. Large companies revel in Linux because of its advantages and usefulness, and so the kernel and various distributions will always exist as the best alternative operating system.
