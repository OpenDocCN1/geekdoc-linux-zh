# 172APPENDIX D. INTRO TO ALPHA SYSTEMS AND PROCESSORS

# D.2 What is Digital Semiconductor

Digital Semiconductor (DS, http://www.digital.com/info/semiconductor/) is the business unit within Digital Equipment Corporation (Digital - we don't like the name DEC) that sells semiconductors on the merchant market. Digital's products include CPUs, support chipsets, PCI-PCI bridges and PCI peripheral chips for comms and multimedia.

# D.3 Alpha CPUs

There are currently 2 generations of CPU core that implement the Alpha architecture:

+   * EV4
+   * EV5

Opinions differ as to what "EV" stands for (Editor's note: the true answer is of course “Electro Vlassic” See section D.12), but the number represents the first generation of Digital's CMOS technology that the core was implemented in. So, the EV4 was originally implemented in CMOS4. As time goes by, a CPU tends to get a mid-life performance kick by being optically shrunk into the next generation of CMOS process. EV4S, then, is the EV4 core implemented in CMOS5 process. There is a big difference between shrinking a design into a particular technology and implementing it from scratch in that technology (but I don't want to go into that now). There are a few other wildcards in here: there is also a CMOS4S (optical shrink in CMOS4) and a CMOS5L.

True technophiles will be interested to know that CMOS4 is a 0.75 micron process, CMOS5 is a 0.5 micron process and CMOS6 is a 0.35 micron process.

To map these CPU cores to *chips* we get:

```
/21064-150,166/ EV4 (originally), EV4S (now)
/21064-200/ EV4S
```