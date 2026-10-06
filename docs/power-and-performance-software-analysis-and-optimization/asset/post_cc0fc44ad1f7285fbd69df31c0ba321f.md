
# Introduction

A software engineer spends enough time writing software with others, the engineer will eventually hear, or perhaps remark to a colleague, the widely misused quote from Donald Knuth, “premature optimization is the root of all evil” (Knuth, 1974).

In order to understand this quote, it is necessary to first establish its context. The original source is a 1974 publication "Structured Programming with Go Statements" from the ACM's Computing Surveys journal. In one of the examples, Knuth notes a performance optimization, which he says, "In established engineering disciplines 12% improvement, easily obtained, is never considered marginal ..." (Knuth, 1974). Clearly Knuth didn't mean, as that all optimizations are, only premature optimizations. This continues, raises the question of what constitutes a premature optimization. Knuth continues, "It is a mistake to make a priori judgements about what parts of a program are really critical..." (Knuth, 1974). In other words, a premature optimization is one made without first analyzing the program to determine.

These words might be more true today than they did back in 1974. Modern systems are significantly more complex, with advances in optimizing compilers, stacked caches, hardware prefetching, out-of-order execution, and countless other logical innovations widening the gap between the code we write, and how our code executes, and subsequently performs. As engineers we must heed Knuth’s warning and ensure that our optimizations target the critical code.

Since an optimization requires analysis, does that mean that all optimization should wait until the software is completely written? Obviously not, because that time will be too late to undo any inefficiencies designed into the core architecture.

In the early stages of architecture and design, performance considerations should revolve around the data structures used and the subsequent algorithms that accompany them. This is an area where Big-O analysis is important, and there should be a general understanding of what algorithms be computationally challenging. For those unfamiliar with Big-O analysis, it is a method for categorizing, and comparing, algorithms by the order of growth in relation to their best, average, and worst cases of input. Early performance measurements can also be obtained from models and prototypes.

As architecture manifests as code, performance profiling should occur to verify that these methods are accurate. Big-O analysis alone is not sufficient. Consider the canonical case of quicksort versus mergesort and heapsort. Mergesort and heapsort are in the worst-case superlinear, which are often outperformed by quicksort, which is in the worst-case quadratic.

# THE ROADMAP

So hopefully, you now have a basic understanding of why performance analysis and optimization is important, and when it is appropriate. The rest of this book focuses on the how and the where. The following content is divided into four parts. The first part provides the necessary background information to get you started, focusing on Intel® Architecture and the interactions between the hardware and the Linux software stack. The second part begins by covering performance analysis methodologies. Then it provides instructions on utilizing the most popular performance profiling tools, such as Intel® VTune™ XE and perf. The third part outlines some of the various common performance problems, identified by the tools in Part 2, and then provides details on how to correct them. Since each performance situation is different, this part is far from comprehensive, but is designed to give the reader a starting point.

Throughout this book, AT&T syntax is used for instructions. Hexadecimal numbers are prefixed with 0x, binary numbers are written with a subscript, such as 001₂, and all other numbers are in base ten.

# PART 1: Background Knowledge

## CHAPTER 1 Early Intel® Architecture

### CONTENTS
- 1.1 Intel® 8086 ........................................................................ 5
  - 1.1.1 System State ................................................................... 7
    - Address Space ........................................................................ 7
  - 1.1.2 Registers ....................................................................... 8
  - 1.1.3 Instructions .................................................................... 10
    - Data Movement ................................................................. 11
    - Integer Arithmetic ................................................................ 11
    - Boolean Logic ............................................................. 12
    - Flow Control ......................................................................... 12
    - String ......................................................................... 12
  - 1.1.4 Machine Code ...................................................... 13
- 1.2 Intel® 8088 ........................................................................ 16
  - 1.2.1 IEEE 754 Floating Point ................................................ 16
    - Formats, Precision, and Environment ............................... 18
    - Support ......................................................................... 19
  - 1.2.2 x87 Floating Point ........................................................ 20
- 1.3 Intel® 80286 ....................................................... 20
  - 1.3.1 Protected and Real Mode ............................................... 21
  - 1.3.2 Protected Mode Segmentation ................................. 21
  - 1.3.3 Task Control ......................................................... 22
- 1.4 Intel® 80386 ....................................................... 23
  - 1.4.1 32-Bit Mode ................................................... 24
  - 1.4.2 Paging ................................................................... 26
- References ................................................................................ 28

The power button is pressed, causing the #RESET pin to be asserted, the voltage is driven into the predefined threshold that represents the active logic level. After a predefined number of clock cycles passes, the #RESET pin is then deasserted, invoking the hardware reset. The hardware reset is responsible for initializing the processor to a known state. This includes setting the general purpose, control and status registers to their documented initial values.

This first “breath” leaves the processor in an execution state significantly different from the one which most developers are familiar. The processor begins execution in 16-bit Real-Address mode. This journey between 16-bit Real-Address mode and 64-bit, or 32-bit, Protected Virtual-Address mode occurs every time the processor is powered on. In doing so, this process mirrors the historical evolution of the Intel® Architecture, from the 16-bit 8086 of 1978 to the 64-bit Intel® Core™ processor family of the twenty-first century. As the computer is booted, more than 40 years of advancements in processor technology unfold in the blink of an eye.

The author imagines some readers are wondering what benefit could possibly come from the retention of all these relics of computing antiquity in modern processor design. Backwards compatibility, by definition involves older designs, directly benefit the reader. As readers, hopefully, continue through this book, they will find references to many architectural features. Education on usage of these features is an investment of the reader’s time. By strictly maintaining backward compatibility, Intel ensures that the investments made by the reader today continue to pay dividends for the foreseeable future. Consider that original bytecode compiled in the late 1970s will still run unmodified on a modern Intel® processor fabricated in 2014.

Other detractors argue that Intel Architecture is inelegant. Since elegance is in the eyes of the holder, this claim is hard to refute. The author is not a hardware engineer; as a software engineer, the author sees an interesting parallel between hardware and software in this claim. Many software projects are architected to be elegant to a well-defined problem. The elegance erodes over time as new features, which were unimaginable during the design phase, are requested and bug fixes and workarounds are introduced. After enduring these unavoidable harsh realities of the software lifecycle, a software’s worth comes from elegance but from whether software works, is still reliable, and can still be extended to future needs. The author submits that x86 still works, is still reliable, and can still be extended.
