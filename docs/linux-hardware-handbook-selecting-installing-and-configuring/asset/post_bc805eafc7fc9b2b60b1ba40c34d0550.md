
# PART I

RIMMs are also unusual in that empty RIMM sockets on a motherboard must be filled with a *continuity module*. With earlier memory types, empty sockets were well—empty. The design of RIMMs, however, requires an electrical connection between certain pins, even when the socket isn't in use, and this connection is provided by a dummy RIMM continuity module. If you get a motherboard that takes RIMM memory, don't remove the continuity modules except to insert RAM, and don't discard modules you've removed—you might need them should you trade in two or more low-capacity RIMMs for a single higher-capacity model.

## Error Detection and Correction

SIMMs and DIMMs support two major forms of error handling: Error detection (*parity*) and error *correcting code* (ECC). Parity memory allows the computer to detect an error, but it can't do anything about that error, so the result is usually a system crash. In some cases this can be worse than using corrupt data, but the problem is that without parity, you can't *trust* your data—the spreadsheet that contains your income tax information, the raw data for your dissertation, or whatever might or might not be accurate if you have no error detection circuitry.

ECC goes one step further; it can not only detect, but also correct, 98% of memory errors. This results in smoother computer operation and little doubt concerning the veracity of the data on your computer—or at least, little need to worry that it's been scrambled by a memory error.

Both parity and ECC require more memory, however. Specifically, parity requires one extra bit per byte. Rather than using 8 bits to store one byte of information, 9 bits are required—8 bits for the data, 1 bit for the parity information. For ECC, the equation is more complex, and depends on the width of the memory bus. For 80486 systems, ECC requires 7 bits per 32-bit transfer, but in Pentium-class systems and above, 8 bits per 64-bit transfer are required. Thus, ECC in Pentium-class and later systems takes the same amount of extra memory as does parity, and, in fact, you can use parity SIMMs or DIMMs in either parity or ECC modes, assuming your motherboard supports both options.

Although parity imposes no special speed penalty, ECC does. Reads from ECC RAM are as fast as reads from ordinary RAM, but writes require computations that slow memory access slightly—by a few percent at most.

Unfortunately, most SIMMs and DIMMs sold today don't support parity, and many motherboard chipsets don't support parity or ECC (see Tables 2.1 through 2.4 for information on parity and ECC support in many chips). If you're building your own system or buying a new one built to specification, it's well worth seeking out parity or, especially, ECC. This is particularly true if you use the computer in some critical capacity or in a role where you expect it to run without crashing for a long period, such as a server.

RDRAM, and hence RIMMs, support an optional parity bit, which can be used for either parity or ECC. RDRAM technology is new enough that it's unclear how common use of parity or ECC will become with RIMMs.

# Memory Electrical Types

The preceding section described the various physical characteristics of assorted memory types—SIMMs, DIMMs, and RIMMs. With the exception of RIMMs, each memory module type can hold any of several different RAM chip variants. These variants differ in their electronic characteristics, their maximum access speeds, and so on.

## FPM DRAM

One of the earliest types of RAM was *fast page mode* (FPM) dynamic RAM (DRAM). FPM refers to the capability of RAM to make consecutive accesses to the same area (that is, the same *page*) of a RAM chip more quickly than the first access. This timing is often represented by a series of numbers indicating the number of cycles for each access. Typical FPM memory operates on 5-3-3-3 timing. Assuming a 66MHz system bus (and hence 1/66,000.000 = 15ns cycle time), the first access takes 5x15ns, and each subsequent access takes 3x15ns, for a total of 210ns. Without taking advantage of FPM timing, the total would be 4x5x15ns, or 300ns.

FPM DRAM was used on most 80486 and Pentium systems from 1995 and earlier. It has become quite rare since then, because more advanced memory types are no more expensive to produce, and might be less expensive to purchase because of supply and demand forces in the marketplace. FPM DRAM is available in 30- and 72-pin SIMM formats.

## EDO DRAM

*Extended data out* (EDO) DRAM was the next major advance in memory technology that found its way onto x86 motherboards. EDO's speed improvement derives from the fact that EDO allows consecutive memory accesses to overlap each other slightly. Expressed in terms of memory timing, EDO allows 5-2-2-2 timing, rather than the 5-3-3-3 typical of FPM DRAM. This translates into 165ns per four memory accesses, versus 210 for FPM DRAM.

EDO DRAM requires specific support in the motherboard's chipset, so you can't simply drop EDO DRAM memory modules into a motherboard designed to use FPM DRAM. EDO DRAM is most commonly found in 72-pin SIMM format, but early DIMMs also used EDO DRAM. This memory format was most commonly used between 1995 and 1997.

One variant on EDO DRAM is *Burst EDO* DRAM. Burst EDO never caught on in the marketplace, although a few chipsets did support it.

## SDRAM

In early 2000, the most common type of memory used on computer motherboards is *synchronous DRAM* (SDRAM). SDRAM runs in synchronization with the system bus, unlike earlier memory types, which relied on *wait states* to allow the memory system to catch up with the system bus. Therefore, SDRAM allows memory access times of 5-1-1-1, or 120ns for four accesses on a 66MHz bus.

With the advent of motherboard busses run at speeds higher than 66MHz, SDRAM speeds had to increase. That is, SDRAM used on a 100MHz bus (as an example) has to be able to complete its accesses faster than SDRAM on a 66MHz bus—four accesses in 80ns, rather than 120ns. These faster SDRAM versions aren't different from 66MHz SDRAM in any fundamental way, but they do have special names: *PC100* and *PC133*. Each name includes a number corresponding to the maximum speed of a motherboard bus on which the RAM can be used. There's no problem in using PC133 SDRAM on a 100MHz or even a 66MHz system bus, so if you're in the market for SDRAM, it might make sense to buy the PC133 variety—but you'll pay a little more for it than for PC100 SDRAM.

SDRAM is usually sold on DIMMs. In fact, most DIMMs sold in 2000 are SDRAM; the older EDO DRAM DIMMs are quite rare today. Because most computers that accept DIMMs can use SDRAM, this doesn't pose compatibility problems when outfitting a motherboard with entirely new RAM.

**CAUTION**

Most motherboards don't allow you to mix SDRAM and EDO DRAM. Therefore, if you have a computer that uses older EDO DRAM DIMMs, you must either replace those DIMMs with larger SDRAM DIMMs or track down and purchase EDO DRAM DIMMs if you want to expand your computer's memory.

One potentially important variant of SDRAM is known as *double data rate SDRAM* (DDR SDRAM). DDR SDRAM operates by allowing *two* transfers per clock cycle, effectively doubling the speed of RAM. An assortment of chipset and CPU manufacturers, including AMD, SiS, and VIA, are promoting DDR SDRAM. Intel, by contrast, is promoting RDRAM, which offers a slightly greater speed increase. RDRAM is a patented technology requiring license fees, whereas DDR SDRAM is not so encumbered.

## RDRAM

RDRAM is the latest form of memory to make its way onto x86 motherboards. As described earlier in this chapter, RDRAM is used exclusively on RIMMs; these memory modules were designed specifically for RDRAM.

RDRAM is unusual in that it incorporates its own bus. Previous memory technologies linked the RAM chips more-or-less directly to the memory bus controlled by the motherboard's chipset, which in turn linked fairly seamlessly to the CPU's memory bus. RDRAM adds another bus to the equation. This bus transfers 16 bits at a time, but operates much faster than the CPU's RAM bus. In early 2000, most CPUs run at an external clock rate of 100MHz and transfer 64 bits per memory access. RDRAM's Rambus, by contrast, operates at 800MHz. Even with only 16 bits per transfer, RDRAM is twice as fast as conventional SDRAM. In fact, RDRAM incorporates additional tricks to bring effective RAM speed close to three times that of PC100 SDRAM.

An RDRAM RIMM has its own internal structure, consisting of a 128-bit wide bus split into eight 16-bit banks. Each bank itself operates at 100MHz, hence the 800MHz total speed (8 banks × 100MHz = 800MHz). The internal operation at 100MHz means that the RAM chips used by RDRAM need not be substantially more technologically advanced than SDRAM; they're simply harnessed in parallel to produce greater net speed.

RDRAM is rare in early 2000, but is expected to become more common as the year wears on. Its greater speed will be a virtual necessity as CPU bus speeds increase. Recent Intel motherboard chipsets use RDRAM (refer to Table 2.2 for details). Because RDRAM requires support for the Rambus technology in the motherboard chipset, it won't become common until most motherboards support it.

# Exotic and Non-Motherboard RAM Types

In addition to these mainstream RAM types, others exist. Some, such as Burst EDO DRAM, are variants on these common types. Others are used in specialized applications. For instance, video cards require their own RAM, and various forms of RAM specialized for this application have emerged, as discussed in the section titled "Video RAM" in Chapter 12.

# Matching Memory to the Motherboard

If you're looking to upgrade the memory on an existing computer, you might think you now know enough to do the job. Sadly, this might not be the case, because additional RAM characteristics can disrupt an otherwise sound RAM match. Typically, if you mismatch some additional factor, you get unreliable computer operation, although in some cases the computer fails to recognize the RAM. In rare cases, you might even damage the motherboard or the RAM.

# Checking Supported Memory Speed

Until PC100 and PC133 SDRAM came along, memory speed was measured in nanoseconds (ns). Indeed, even PC100 and PC133 RAM speed is measured in ns; it's just that the names
