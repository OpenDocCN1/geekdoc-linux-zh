
![](img/53ede4f4266a5731b93bff15d85fa06a_31_0.png)

**Figure 1.3** Example application architecture. Application code uses a timer to act periodically, sensors to collect data, and a routing layer to deliver data to a sink.

can be reprogrammed without needing to collect all of the nodes. However, these four abstractions – power control, timers, sensors, and data collection – encompass the entire datapath of the application.

## 1.4 Compiling and installing applications

You can download the latest TinyOS distribution, the nesC compiler, and other tools at www.tinyos.net. Setting up your programming environment is outside the scope of this book; the TinyOS website has step-by-step tutorials to get you started. One part of TinyOS is an extensive build system for compiling applications. Generally, to compile a program for a sensor platform, one types `make <platform>`, e.g. `make telosb`. This compiles a binary. To install that binary on a node, you plug the node into your PC using a USB or serial connection, and type `make <platform> install`. The tutorials go into compilation and installation options in detail.

## 1.5 The rest of this book

The rest of this book goes into how to program in nesC and write TinyOS applications. It is divided into three parts. The first is a short introduction to the major programming concepts of nesC. The second part addresses basic application programming using standard TinyOS APIs. The third part is a little deeper, and looks into how those TinyOS APIs are implemented. For example, the third part describes how TinyOS abstracts hardware, so you can write a driver for a new sensor.

Chapter by chapter, the book is structured as follows:

- **Chapter 1** is this chapter.
- **Chapter 2** describes the major way that nesC breaks from C and C-like languages: how programs are built out of components, and how components and interfaces help manage programs’ namespaces.
- **Chapter 3** presents components and how they interact via interfaces.
- **Chapter 4** goes into greater detail into configurations, components which connect other components together.
- **Chapter 5** covers the basic TinyOS execution model and gives guidance on how and when to use tasks.
- **Chapter 6** takes the material from the prior three chapters and brings it together into an example of writing a fully-fledged application that sends an alarm when a node observes a change in its environment. In the process, it covers the major TinyOS APIs (timing, sensing, communication, and storage).
- **Chapter 7** details the PC-side tools for communicating with nodes connected over the serial port, and covers the TinyOS serial stack and packet formats.
- **Chapter 8** introduces more advanced component topics, such as parameterized interfaces and attributes. While applications typically don’t use these mechanisms, they are indispensable when writing reusable libraries and systems.
- **Chapter 9** goes into wiring parameterized interfaces, which form the basis for most reusable systems. After describing the basic mechanisms for managing interface keys, it goes through four examples of increasing complexity.
- **Chapter 10** presents eight common TinyOS design patterns: commonly useful and powerful ways of organizing components.
- **Chapter 11** concludes the advanced programming topics by covering concurrency. It describes asynchronous code, the TinyOS task model, and power locks.
- **Chapter 12** describes the Hardware Abstraction Architecture (HAA), the three-level hierarchy TinyOS uses to raise low-level hardware abstractions to hardware-independent, application-level services.
- **Chapter 13** goes step-by-step through an advanced application that identifies the location of an event based on when nodes sense it. It uses lower-layer interfaces to implement time synchronization and high-frequency sampling.
- **Appendix** gives a concise overview of major TinyOS application interfaces.

Throughout the book, you will find *programming hints*: general best-use practices that we’ve distilled from the many users of TinyOS and nesC. These are all listed on the sheet at the front of the book.

Finally, the complete source code for example applications presented in this book (in Chapters 6, 7 and 13) is available in TinyOS’s contributed code directory, under the name “TinyOS Programming” – see www.tinyos.net for details.
