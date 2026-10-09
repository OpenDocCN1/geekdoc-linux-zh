+   - Object Features
- Extending Objects
- Special Forms
- Language Support
- **Summary: Object-Oriented Thinking**

The battery in a clock supplies the clock the power it needs to run. If you need to replace the battery, you simply take one out and put in a new one. Imagine how easy it would be if we could do the same thing with programs—simply unplug the old and plug in the new.

Object technology attempts to reach that level of interfacing. It focuses on the responsibility of each component and provides a solid and unchangeable interface to which you can connect other components. To understand where the technology is going, you need to know where it has been.

This chapter covers the concepts behind object technology. It does not cover the wide expanse of all the theory, but it does introduce the main topics. It begins with the evolution of software engineering and concludes with ways to apply these concepts to non-object-oriented languages.

# **NOTE**

This chapter precedes the chapters that discuss sockets in specific implementations. In order to cover properly the specific implementations in Java and C++, this chapter provides foundational information about objects. No book on objects should omit the foundational philosophies as a preamble. Generally, most programmers do not understand objects, so implementations skew slightly from the original intent of the technology.

# The Software Engineering Evolution

The development of software and programming does not have the lengthy history of physics, mathematics, or other such sciences. One part of software engineering (the lifecycle of software development)—computer science—relies heavily, however, on the thought and process of mathematics, particularly Boolean algebra, group theory, and statistics. Still, the software engineering and computer science fields have made significant strides in technology. These strides have defined how you use your computer today.

After you understand how these pieces fit together, you can easily choose the right tools for the right job. This section describes each type of programming and modeling theory that the industry has developed over the last few decades. Essentially, the strides (or stages) in technology encompass each other as an expanding set of tools and methodology. The most significant stages are Functional, Modular, Abstract, and Object Programming. This section describes each stage.

# Step-by-Step Functional Programming

The first method development came from the concept of flowcharting. The whole idea was that every program included a series of functions, decisions, data, and I/O. Flowcharts show the step-by-step stages of evaluation, transforming meaningful input into meaningful output.

Functional design evolved into Structured System Requirements (SSR), Structured System Analysis (SSA), and Structured System Design (SSD). Each phase defines the materials needed to solve a