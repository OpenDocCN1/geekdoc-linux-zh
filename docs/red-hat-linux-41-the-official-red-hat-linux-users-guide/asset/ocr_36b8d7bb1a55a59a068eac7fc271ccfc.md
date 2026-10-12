176 APPENDIX D. INTRO TO ALPHA SYSTEMS AND PROCESSORS

# ## D.5 A Few Notes On Clocking

All of the current Alpha CPUs use high-speed clocks, because their microarchitectures have been designed as so-called short-stick designs. None of the system busses have to run at horrendous speeds as a result though:

+   - on the 21066(A), 21064(A), 21164 the off-chip cache (Beache) timing is completely programmable, to the resolution of the CPU clock. For example, on a 275MHz CPU, the Beache read access time can be controller with a resolution of 3.6ns
+   - on the 21066(A), the DRAM timing is completely programmable, to the resolution of the CPU clock (*not* the PCI clock, the CPU clock).
+   - on the 21064(A), 21164(A), the system bus frequency is a sub-multiple of the CPU clock frequency. Most of the 21064 motherboards use a 33MHz system bus clock.
+   - Systems that use the 21066 can run the PCI at any frequency relative to the CPU. Generally, the PCI runs at 33MHz.
+   - Systems that use the APECS chipset (see Section D.6) always have their CPU system bus equal to their PCI bus frequency. This means that both busses tends to run at either 25MHz or 33MHz (since these are the frequencies that scale up to match the CPU frequencies). On APECS systems, the DRAM controller timings are software programmable in terms of the CPU system bus frequency

*Aside:* someone suggested that they were getting bad performance on a 21066 because the 21066 memory controller was only running at 33MHz. Actually, it’s the superfast 21064A systems that have memory controllers that ‘only’ run at 33MHz.

# ## D.6 The chip-sets

DS sells two CPU support chipsets. The 2107x chipset (aka APECS) is a 21064(A) support chipset. The 2117x chipset (aka ALCOR) is a 21164 support chipset. There will also be 2117xA chipset (aka ALCOR 2) as a 21164A support chipset.