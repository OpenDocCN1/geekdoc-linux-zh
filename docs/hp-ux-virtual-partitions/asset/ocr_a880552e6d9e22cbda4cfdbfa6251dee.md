# CHAPTER 3

# Booting and vPars

# vpmon, vparload, vparboot, PDC, ISL,
hpux, Secure Web Console, GSP
Configuration

# Background

We have already done a lot of work on our system in previous chap-
ters to load and configure HP-UX 11i and Virtual Partitions (vPars.)
Now let's take a step back and examine the details of booting an HP
9000. After having loaded vPars onto a system there are some modifi-
cations in the boot process. Let's cover booting with vPars and then
examine booting in general later in the chapter. First we'll cover boot-
ing after vPars have been installed on a system to see the impact that
vPars have on the boot process. And then in the non-vPars-specific
portion of this chapter you'll get an overview of: the low-level boot
and configuration of an HP 9000; setting up HP Secure Web Console;
and configuring the Guardian Service Processor (GSP).

Most of the systems used in the examples in this chapter for both
the vPars-specific and non-vPars-specific sections are L-Class sys-
tems. I intentionally used a simple system so that we could concen-
trate on the boot process with a minimum amount of hardware-related
messages. Since booting varies from system to system, even within