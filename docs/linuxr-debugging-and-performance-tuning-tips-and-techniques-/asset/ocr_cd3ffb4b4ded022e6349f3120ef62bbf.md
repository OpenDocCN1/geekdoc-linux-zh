it’s much better.” GNU software is generally more robust, and performs better, than standard Unix versions. In this section we look at some of the reasons why, and at the document that describes the principles of GNU software design.

The *GNU Coding Standards* describes how to write software for the GNU project. It covers a range of topics. You can read the *GNU Coding Standards* online at http://www.gnu.org/prep/standards.html. See the online version for pointers to the source files in other formats.

In this section, we describe only those parts of the *GNU Coding Standards* that relate to program design and implementation.

# 1.4.1 Program Design

Chapter 3 of the *GNU Coding Standards* provides general advice about program design. The four main issues are compatibility (with standards and Unix), the language to write in, reliance on nonstandard features of other programs (in a word, “none”), and the meaning of “portability.”

Compatibility with Standard C and POSIX, and to a lesser extent, with Berkeley Unix is an important goal. But it’s not an overriding one. The general idea is to provide all necessary functionality, with command-line switches to provide a strict ISO or POSIX mode.

C is the preferred language for writing GNU software since it is the most commonly available language. In the Unix world, Standard C is now common, but if you can easily support Original C, you should do so. Although the coding standards prefer C over C++, C++ is now commonplace too. One widely used GNU package written in C++ is groff (GNU troff). With GCC supporting C++, it has been our experience that installing groff is not difficult.

The standards state that portability is a bit of a red herring. GNU utilities are ultimately intended to run on the GNU kernel with the GNU C Library.7 But since the kernel isn’t finished yet and users are using GNU tools on non-GNU systems, portability is desirable, just not paramount. The standard recommends using Autoconf for achieving portability among different Unix systems.

7 This statement refers to the HURD kernel, which is still under development (as of early 2004). GCC and GNU C Library (GLIBC) development take place mostly on Linux-based systems today.