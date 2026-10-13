tained herein. Thus, we have emphasized the methods and tools that can be used on a Solaris system to extract information that otherwise is not easily accessible with the standard bundled commands and utilities. We want to illustrate how you can apply this knowledge in a meaningful way, as your job or interest dictates.

To maximize the usefulness of the text, we included specific information on Solaris versions 2.5.1, 2.6, and Solaris 7. We cover the major Solaris subsystems, including memory management, process management, threads, files, and file systems. We do not cover details of low-level I/O, device drivers, STREAMS, and networking. For reference material on these topics, see “Writing Device Drivers” [28], the “STREAMS Programming Guide” [29], and “UNIX Network Programming” [32].

The material included in this book is not necessarily presented at an introductory level, although whenever possible we begin discussing a topic with some conceptual background information. We assume that you have some familiarity with operating systems concepts and have used a Unix-based operating system. Some knowledge of the C programming language is useful but not required.

Because of the variety of hardware platforms on which Solaris runs, it is not practical to discuss the low-level details of all the different processors and architectures, so our hardware focus, when detail is required, is admittedly UltraSPARC-centric. This approach makes the most sense since it represents the current technology and addresses the largest installed base. In general, the concepts put forth when detail is required apply to other processors and platforms supported. The differences are in the specific implementation details, such as per-processor hardware registers.

Throughout the book we refer to specific kernel functions by name as we describe the flow of various code segments. These routines are internal to the operating system and should not be construed as, or confused with, the public interfaces that ship as part of the Solaris product line—the systems calls and library interfaces. The functions referenced throughout the text, unless explicitly noted, are private to the kernel and not callable or in any way usable by application programs.

# Intended Audience

We hope that this book will serve as a useful reference for a variety of technical staff members working with the Solaris Operating Environment.

+   - **Application developers** can find information in this book about how Solaris implements functions behind the application programming interfaces. This information helps developers understand performance, scalability, and imple-