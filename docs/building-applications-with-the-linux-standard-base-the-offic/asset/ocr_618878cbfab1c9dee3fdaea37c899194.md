+   • Following the LSB packaging guidelines
+   • Seeking LSB certification

The following sections describe each of these steps in detail.

# 2.1.1 Coding to the Portability Layer

Rather than let applications access operating system resources directly, open systems such as UNIX and Linux have a portability layer for applications to be coded to. For UNIX, this coding layer is the set of POSIX application programming interfaces (APIs). However, since we know that “GNU’s Not UNIX,” the LSB has referenced POSIX for Linux in the form of the LSB Written Specification standard (Figure 2.1).

Applications must not use private interfaces of the operating system, or subvert the portability layer by accessing operating system resources directly. Some applications access system resources directly in order to be *platform-tuned*. Platform-tuning of an application may increase performance, but it greatly diminishes the possibility that the software will be binary compatible between systems or releases. This kind of software is sometimes platform-branded to work for a particular release of an operating system, which is fine

![](bbox=[0.13, 0.65, 0.85, 0.86])