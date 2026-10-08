# Introduction to digital forensics

Digital forensics (also known as cyber forensics or just forensics) is the process used to collect, identify, gather, secure, and store data from digital systems that can be used as evidence.

In our case, we will focus on forensics to detect the use, abuse, intrusion, damage, or modification of computer systems, servers, networks, infrastructures, or data. However, forensics is also used to recover deleted or modified data, so let's take a few minutes to review how forensics can be used for that.

# Forensics to recover deleted or missing data

There is one part of forensics that is used to collect, identify, and recover deleted data from digital media.

Usually, data is recovered from non-volatile media storage such as hard drives and USB drives, but it is also possible to gather data from volatile memory as Random Access Memory (RAM).

Volatile versus non-volatile memory
Volatile memory such as RAM is a type of memory that only saves the information while it is ON, while non-volatile memory such as hard drives can retain information over a very long time, even when they have no power. Therefore, gathering information from volatile memory is considered a more complex and specialized task.

Now, let's start by reviewing how to capture data from volatile memory.

# Recovering data from RAM

Due to the hardware nature of RAM, recovering data from RAM is considered a very complex task. However, there is one tool and one method we can use to achieve this goal. Let's take a look.

# Microsoft COFEE

The Microsoft Computer Online Forensics Evidence Extractor (COFEE) toolkit was developed and distributed by Microsoft to police agencies to help them collect digital evidence from Microsoft systems.

The tool is loaded as a live USB and is composed of a Graphical User Interface (GUI) with more than 150 forensics tools, including data stored on volatile memory (RAM).