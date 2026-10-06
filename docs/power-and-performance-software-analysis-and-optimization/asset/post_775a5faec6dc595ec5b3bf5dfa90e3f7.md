
| 7 | 6 | 4 | 2 | 0 |
|---|---|---|---|--|
| 0 | Output | Polarity | Aggregation | Source size |

FIGURE 16.1
PCMPxSTRY immediate operand.

of the strings are only relevant to the instruction with regard to the values loaded into the SIMD registers, both lengths loaded into these general purpose registers are internally saturated, although the values stored in the actual registers aren't affected, to the maximum width of the SIMD register. This fact can be exploited in order to reduce the number of registers required for some string operations by also using the explicit length registers as counters.

The second variable, the y variable, in the PCMPxSTRY controls the output format. This variable can be either the character "I" for index or "M" for mask. In index mode, the result is stored into the ECX register. In mask mode, the result of each comparison is stored in the destination operand as a mask.

Therefore, the four PMPSTRY instructions are defined as follows:

- PCMPESTRI Compares two explicit length strings, whose lengths are in RDX/RAX or EDX/EAX and stores the result in ECX.
- PCCMPSTR Compares two explicit length strings and stores the result in the destination SIMD register.
- PCMPISTRI Compares two implicit length strings, stopping at the first NULL byte, and stores the result in the ECX.
- PCMPISTR Compares two implicit length strings, and stores the comparison result in the destination SIMD register.

The PCMPSTRY instructions are designed to handle a lot of different scenarios. As a result, the first operand is an 8 bit immediate that controls the exact behavior of the comparison. This includes whether the comparisons occur between unsigned characters or words, what should be reported, and so on. Figure 16.1 in order to communicate additional information about the result, the arithmetic flags in the EFLAGS are overloaded with special meanings.

## 16.4.1 FURTHER READING

- https://software.intel.com/en-us/articles/schema-validation-with-intel-streaming-simd-extensions-4-intel-sse4

## Index

Note: Page numbers followed by $f$ indicate figures and $t$ indicate tables.

## A

- ABI. See Application Binary Interface (ABI)
- Advanced Configuration and Power Interface(ACPI) specification
- AML interpreter, 44
- C state, 46–48
- definition, 44
- EIST, 45
- P states, 45–46
- T states, 44–45
- Apitrice, 185–187, 186/$f$
- Application Binary Interface (ABI) calling conventions, 215–216
- definition, 214
- natural alignment, 215
- Array of structures (AOS), 267–269
- Asymmetric mode, 50
- level 1 (L1) cache, 251
- level 2 (L2) cache, 251
- level 3 (L3) cache, 251
- LLC, 250, 251
- prefetching, 256–257
- storage hierarchy, 249, 250/$f$
- sysfs interface, 256
- temporal data locality, 249
- FLAGS. See compiler flags (CFLAGS)
- CISC. See Complex Instruction Set Computer (CISC)
- Clock times, 32–84
- algorithmic/microarchitectural analyses, 123 analysis type, 123
- command-line interface, 123–124
- configuration, 125–127
- graphical interface, 124, 124/$f$
- results directory, 124
- XML file, 123
- Command-line interface analysis type (see *Collect action*)
- apitrrice, 185
- callbacks report type, 128
- finalize action, 127
- general-exploration analysis, 128–129
- grep-c report type, 128
- hotspots report type, 128
- Phorix Test Suite, 88–87
- result-dir arguments, 127–128
- summary report type, 128
- sysprof-module, 260
- top-down report type, 128
- Compiler flags (CFLAGS), 207–209, 207/$f$
- Complex Instruction Set Computer (CISC), 35–36

## B

- BIU. See bus unit (BIU)
- blk tracer, 171–174, 172/$f$
- Branching
- CC instruction, 243–244, 245
- CMP instruction, 245
- conditional branch, 239
- JCC instruction, 243–244, 245
- masks, 241
- optional code, 241
- prediction accuracy, 240–241
- profiled guide optimization, 246–247
- shift instructions, 242
- store calculation, 242, 243
- speculative execution, 239–240
- unconditional branch, 239
- Bus unit interface (BIU), 6–7

## C

- associative cache, 251
- cache hit, 249
- cache line, 251–252
- cache miss, 249
- CPUID, 253–256
- data locality, 257–259
- dcache, 251
- icache, 251
- CPU migrations, 66–77
- disk performance, configurability of, 75
- HTML page, 74–75
- microbenchmarks, 74
- mmap(2) system, 76
- noisy system, 76
- P and C state, 75
- remote resources, 75
- tmpfs file, 75–76
- Control unit (CU), 20
- Counted event configuration, 143–144
- code snippet, 82
- frequency, 80
- TSC, 80–82
- CPU cycles
- CPU dispatch
- CPUID, 217–220
- CPU dispatch, 217–220
- runtime dispatch, 222–225
- CPU Identification (CPUID), 217–220, 253–256
- CRC32, 275
- Downloads.xml, 96
- install.sh, 96–97
- new directory, 95
- results-definition.xml, 97
- support-check.xml, 96
- test-definition.xml, 95–96

## E

- ELF, See Executable and Linkable Format (ELF)
- Enhanced SpeedStep® technology (EIST), 45
- Event configuration, 143–144, 145
- Event counters
- APIC interrupt, 106
- bottleneck, 107
- edge bit, 106
- fixed-function, 105
- interface and hardware, 105
- microarchitectural performance analysis, 107
- MSB format, 106
- programmable counters, 107
- user and operating system, 106
- Executable and Linkable Format (ELF)
- executable file, 209
- execution view, 210
- linking view, 209–210
- PIC, 210–214
- relocatable files, 209
- shared objects, 209

## D

- Data collection
- analysis type (see Collect action)
- bug, 152
- command line interface, 123
- configuration option, 122, 122f
- finalize action, 127
- graphical interface, 122
- kernel tool, 175
- Latency, 199
- perf tool, 156
- trace and trace_pipe file, 168
- DebugFS
- available_tracer file, 168
- blk tracer, 171–174, 172/j
- busbox, 166
- current_tracer file, 168
- function and function_tracers, 168–181
- mount(1) command, 167
- nop tracer, 174
- trace and trace_pipe file, 168
- Decoder/cache, 110, 111
- Direct Rendering Infrastructure (DRI)
- bufferinfo, 180
- DRM, 179, 180
- GEM, 180
- KMS support, 180
- Direct Rendering Manager (DRM), 179, 180

## F

- Fixed-function core, 105, 107
- Flex Memory technology, 49–50
- Floating point (FPU), 20
- Firace
- dynamic tracepoints, 165–166
- kernelsh, 174–176, 175/f
- Linux distributions (see DebugFS)
- static tracers, 165–166
- function_graph tracer, 168–171
- function tracer, 168–171

## G

- GEM. See Graphics Execution Manager (GEM))
- Git, 62–63
- cleaning patches, 65–65, 64/f
- sending patches, 65–67, 66/t, 67/j
- Global descriptor table (GOT), 22
- Global Offset Table (GOT), 212–213
- GNU code cover (gcov), 192–193
- GNU compiler toolbar (GCC), See Toolchains
- GNU profiler (gprof)
- binary data file, 190
- compiler profile, 199
- flat profile, 190
- gove, 192–193
- graph profile, 190–192
- limitations, 192
- workload testing, 189–190

GOT. See Global Offset Table (GOT)
- GPU: See Graphics unit (GPU)
- Graphical user interface (GUI)
- analysis type (see Collection action)
- finalization, 127
- Phorix Test Suite, 87–87
- result-dir arguments, 127–128
- summary report type, 128
- sysprof-module, 260
- top-down report type, 128
- Compiler flags (CFLAGS), 207–209, 207/$f$
- Complex Instruction Set Computer (CISC), 35–36

## I

- IEEE 754 floating point
- IEEE 754 standard (IEEE 754 floating point)
- Instruction-level parallelism (ILP), 32
- Instruction pointer (IP), 213
- ADD instruction, 86, 11
- boolean logic, 12
- data movement, 11
- flow control, 12
- general purpose registers, 8–9
- integer arithmetic, 11–12
- machine code format, 13
- operands, 10–11
- principles, 5–6
- status registers, 9–10
- strings, 12–13
- system diagram, 6
- system state, 5–8
- x86 processor, 5

- Intel Advanced Vector Extensions
(Intel (AVX)), 263–264

- Intel AES Instructions (AES-NI), 273–274

- MMU, 20–21
- protected and real mode, 21
- protected mode generation, 21–22

- Intel 80386 and 8037
- 32-bit mode, 24–26
- Intel kernel splits, 28
- Linux project, 23–24
- logical and linear addresses, 26

- page frame, 26
- PDE and LTE, 26–27
- TLB, 27–28
- Virtual8 mode, 24

- Intel C and C++ Compilers (ICC), 220, 230, 235
- Intel C4™ processor
- Flex Memory technology, 49–50
- Intel HD graphics, 49

- Intel Xeon® processor, 48, 48/f
- PIPL, 51–52
- Turbo Boost, 50–51
- Intel Graphics Media Accelerators (GMA), 49
- Intel Hyper-Threading Technology, 41

- Intel Pentium® 4
- Hyper-Threading, 41
- IA-32 mode, 38–40
- multi-core processor, 40–41

- Po microarchitecture, 38
- Intel Pentium M processor. See Advanced
Configuration and Power Interface (ACPI)
- sification
- Intel Pentium® Pro
- µops, 35–36
- out-of-order execution, 36–38

- SIMD, 32
- supcalar, 33–34
- Intel Thread Building Blocks (Intel® TBB),
262–263
- Intel® VTune™ Amplifier XE
awker driver, 119
