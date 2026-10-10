# PREFACE

While there are many books about the UNIX kernel in its various versions, this is the first to deal specifically with HP-UX and Hewlett-Packard’s PA-RISC architecture. This book is a technical resource for anyone who has to support HP-UX, write kernel modules, or just wants to know how it all works. It is suitable as a text for a class in operating system concepts or HP-UX internals.

# Chapter 1 PA-RISC 2.0 Architecture

Chapter 1 presents some of the important features of the PA-RISC architecture, still the predominant hardware platform for HP-UX. It covers the register set and how the registers are used, then explains virtual memory concepts, address translation and caching, the mechanisms provided by the architecture to support virtual memory, and some of the most common PA-RISC instructions and their use.

# Chapter 2 Procedure Calling Conventions

This chapter examines the conventions used when calling from one procedure to another: how the stack is used and how stack frames are set up, how the registers are used, how arguments are passed, and how results are returned to the calling process. Stack usage for both narrow and wide modes is explained.

# Chapter 3 The Kernel: Basic Organization

This chapter examines the basic organization of the kernel data structures, both hardware-dependent and hardware-independent. The discussion includes tables, the kernel as a resource