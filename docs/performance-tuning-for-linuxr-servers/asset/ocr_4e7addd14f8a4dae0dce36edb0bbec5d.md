# Introduction

Although an understanding of the methods of tuning the operating system is needed to optimize system workload and response, an equally important aspect of performance tuning is the actual work done in the application code to maximize performance particularly for applications that are the sole purpose of a dedicated system. Applications such as web servers, database servers, or mail servers tend to be the primary application for a system, and performance hinges just as much on the application as it does on the operating system.

This chapter addresses some of the issues of writing a program that will run efficiently. We assume performance tuning of the underlying operating system can improve performance, but we want to concentrate on those aspects of writing and assembling a program that will produce minimal tuning parameterization and maximum performance.

We will discuss general techniques for achieving high performance in programs from general considerations of performance analysis to a discussion of basic design as being a key part of application performance. The C and C++ languages will be used in describing the concepts involved, but these methods and ideas are easily applied to any of the programming facilities available to developers today. The GNU Compiler Collection (**gcc**) compiler will be used, but again the concepts involved can translate to other compilation tools. All the source code will be available, and it should compile in any gcc programming environment.

First, we'll discuss the general principles of performance tuning.