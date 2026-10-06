
# Preface

- Why Is Performance Important?
- Linux: Strengths and Weakness
- How Can This Book Help You?
- Why Learn How to Use Performance Tools?
- Can I Tune for Performance?
- Who Should Read This Book?
- How Is This Book Organized?

## Why Is Performance Important?

If you have ever sat waiting for a computer to do something (while pounding on your desk, cursing, and wondering, "What is taking so long?") you know why it is important to have a fast and well-tuned computer system. Although not all performance problems can be easily solved, understanding why things are slow can mean the difference between fixing the problem in software, upgrading the slow hardware, or simply throwing the whole computer out the window. Fortunately, most operating systems—Linux in particular—provide tools to figure out why the machine runs slowly. By using a few basic tools, you can determine where the system is slowing down and which parts are running inefficiently.

Although a slow system is particularly annoying to end users, application developers have an even more important reason to performance tune applications: An efficient application runs on more systems. If you write sluggish applications that need a zippy computer, you eliminate customers who have slower computers, resulting in a bigger potential user base. In addition, a well-tuned application is usable by more customers; when potential customers must choose between two different applications with similar functionality, they often choose the one that runs faster or is more efficient. Finally, a long-lived application likely goes through several rounds of optimization to cope with different customer demands, so it is crucial to know how to track down performance problems.

If you are a system administrator, you have a responsibility to the users of the system to make sure that it runs at an adequate performance level. If the system runs slowly, users complain. If you can determine the problem and fix it quickly, they stop complaining. As a bonus, if you tune the application or operating system (and thus keep them from having to buy new hardware), you make company bean counters happy. Knowing how to effectively use performance tools can mean the difference between spending days or spending hours on a performance problem.

## Linux: Strengths and Weakness

If you use Linux, maintain it, and develop on it, you are in a strange but good situation. You have unprecedented access to source code, developers, and mailing lists, which often document design decisions after they are made. Linux is an excellent environment in which to find and fix performance problems. This contrasts with a proprietary environment, where it is difficult to get direct access to software developers, may be hard to find discussions about most design decisions, and is nearly impossible to access source code. In addition to this productive environment, Linux also has powerful performance tools that enable you to find and fix performance problems. These tools rival their proprietary counterparts.

Even with these impressive benefits, the Linux ecosystem still has challenges to overcome. Linux performance tools are scattered everywhere. Different groups with different aims develop the tools, and as a result, the tools are not necessarily in a centralized location. Some tools are included in standard Linux distributions, such as Red Hat, SUSE, and Debian; others are scattered throughout the Internet. If you're trying to solve a performance problem, you first have to know the tools you need exist, and then figure out where to find them. Because you also figure out how to use them jointly to determine what is broken, this can be a bit of an art, but becomes easier with experience. Although most of the general strategies can be documented, Linux does not have any guide that tells you how to aggregate performance tools to actually solve a problem. Most of the tools or subsystems have information about tuning the particular subsystem, but not how to use them with other tools. Many performance problems span several areas of the system, and unless you know how to use the tools collectively, you will not be able to fix the problem.

## How Can This Book Help You?

You will learn many things from this book, including the following:

- What the various performance tools measure
- How to use each tool
- How to combine the tools to solve a performance problem
- How to start with a poorly performing system and pinpoint the problem
- How the methods are used to solve real-world problems (case studies)

Using the methods in this book, you can make a well-organized and diagnosed problem description that you can pass on to the original developers. If you're lucky, they will solve the problem for you.

## Why Learn How to Use Performance Tools?

Why should anyone put effort into tuning a system or application?

- A well-tuned system can do more with fewer resources.
- A well-tuned application can run on older hardware.
- A well-tuned desktop can save users time.
- A well-tuned server provides a higher service quality for more users.

If you know how to effectively diagnose performance problems, you can take a targeted approach to solving the problem instead of taking a shot in the dark and hoping that it works. If you are an application developer, this means that you can quickly figure out what piece of code is causing the problem. If you are a system administrator, it means that you can figure out what part of the system needs to be tuned, or upgraded, without wasting time trying different solutions. If you are an end user, you can figure out which applications are lagging and report the problem to the developers (or update your hardware, if necessary).

Linux is at a crossroads. Most of the functionality for a highly productive system is already complete. The next evolutionary step for Linux and its applications is to be tuned to compete with and surpass the performance of other operating systems. Some of this performance optimization has already seen time investments, tuned and optimized the system and code. Other performance optimizations—such as the Native POSIX Thread Library (NPTL), which dramatically improves threading performance; and objectlinking, which improves application startup time—are just starting to be integrated into Linux. Linux is ripe for performance improvements.

## Can I Tune for Performance?

The best thing about performance optimization is that you do not need to know the details of the entire application or system to effectively fix performance problems. Performance optimization requires a complementary set of skills to those of a typical application developer.

You need to be observant and persistent. It takes more of a detective than a programmer to hunt down and eliminate performance problems. It is exhilarating to find and fix these. When you start, performance is terrible. However, you track down the cause, rip it out by the roots, and, if you're lucky, the system then runs twice as fast. *Voilà!*

To get to the *finale*, you must understand the powerful but sometimes confusing world of Linux performance tools. This takes some work, but in the end, it is worth it. The tools can show aspects of your application and system that you never expected to see.

## Who Should Read This Book?

This book helps Linux software developers, system administrators, and end users to use the Linux performance tools to find performance problems in a given system. Beginning performance investigators learn the basics of performance investigation and analysis. Medium to advanced performance investigators, especially those with performance experience on other proprietary operating systems, learn about the Linux equivalents of commands from other systems with which they may already be familiar.

Software developers learn how to pinpoint the exact line of source code that causes a performance problem. System administrators who are performance tuning a system learn about the tools that show why a system is slowing down, and they can then use that information to tune the system. Finally, although not the primary focus of the book, end users learn the basic skills necessary to figure out which applications are consuming all the system resources.
