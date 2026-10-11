88

Core Systems

**PART I**

# ## SDRAM

In early 2000, the most common type of memory used on computer motherboards is *synchronous DRAM* (SDRAM). SDRAM runs in synchronization with the system bus, unlike earlier memory types, which relied on *wait states* to allow the memory system to catch up with the system bus. Therefore, SDRAM allows memory access times of 5-1-1-1, or 120ns for four accesses on a 66MHz bus.

With the advent of motherboard busses run at speeds higher than 66MHz, SDRAM speeds had to increase. That is, SDRAM used on a 100MHz bus (as an example) has to be able to complete its accesses faster than SDRAM on a 66MHz bus—four accesses in 80ns, rather than 120ns. These faster SDRAM versions aren't different from 66MHz SDRAM in any fundamental way, but they do have special names: *PC100* and *PC133*. Each name includes a number corresponding to the maximum speed of a motherboard bus on which the RAM can be used. There's no problem in using PC133 SDRAM on a 100MHz or even a 66MHz system bus, so if you're in the market for SDRAM, it might make sense to buy the PC133 variety—but you'll pay a little more for it than for PC100 SDRAM.

SDRAM is usually sold on DIMMs. In fact, most DIMMs sold in 2000 are SDRAM; the older EDO DRAM DIMMs are quite rare today. Because most computers that accept DIMMs can use SDRAM, this doesn't pose compatibility problems when outfitting a motherboard with entirely new RAM.

CAUTION

Most motherboards don't allow you to mix SDRAM and EDO DRAM. Therefore, if you have a computer that uses older EDO DRAM DIMMs, you must either replace those DIMMs with larger SDRAM DIMMs or track down and purchase EDO DRAM DIMMs if you want to expand your computer's memory.

One potentially important variant of SDRAM is known as *double data rate SDRAM* (DDR SDRAM). DDR SDRAM operates by allowing *two* transfers per clock cycle, effectively doubling the speed of RAM. An assortment of chipset and CPU manufacturers, including AMD, SiS, and VIA, are promoting DDR SDRAM. Intel, by contrast, is promoting RDRAM, which offers a slightly greater speed increase. RDRAM is a patented technology requiring license fees, whereas DDR SDRAM is not so encumbered.

# ## RDRAM

RDRAM is the latest form of memory to make its way onto x86 motherboards. As described earlier in this chapter, RDRAM is used exclusively on RIMMs; these memory modules were designed specifically for RDRAM.