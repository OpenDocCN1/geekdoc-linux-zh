# Chapter 0

# Introduction

So, you want to write a kernel module. You know C, you've written a number of normal programs to run as processes, and now you want to get to where the real action is, to where a single wild pointer can wipe out your file system and a core dump means a reboot.
Well, welcome to the club. I once had a wild pointer wipe an important directory under DOS (thankfully, now it stands for the Dead Operating System), and I don't see why living under Linux should be any safer.
Warning: I wrote this and checked the program under versions 2.0.35 and 2.2.3 of the kernel running on a Pentium. For the most part, it should work on other CPUs and on other versions of the kernel, as long as they are 2.0.x or 2.2.x, but I can't promise anything. One exception is chapter 11, which should not work on any architecture except for x86.

# 0.1 Who Should Read This

This document is for people who want to write kernel modules. Although I will touch on how things are done in the kernel in several places, that is not my purpose. There are enough good sources which do a better job than I could have done.
This document is also for people who know how to write kernel modules, but not yet adapted to version 2.2 of the kernel. If you are such a person, I suggest you look at appendix A to see all the differences I encountered while updating the examples. The list is nowhere near comprehensive, I think it covers most of the basic functionality and will be enough to get started.
The kernel is a great piece of programming, and I believe that programmers should read