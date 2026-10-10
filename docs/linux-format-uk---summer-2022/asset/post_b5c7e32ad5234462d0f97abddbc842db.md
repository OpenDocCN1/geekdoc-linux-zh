
# Into a third dimension

We add some depth to the story and learn about the first, bona fide, GPU.

![](img/f20a68d91e56325c44e9a1405ca1923f_33_0.png)

The first ‘computer GPU’, appearing in 1975, was aimed at vector ‘graphics’ in large mainframes like the CDC 6600. It could do a lot of work in parallel but it had no display capability.

The first ‘graphics card’ was in 1984 (above), a replacement part of the Apple Lisa. It used to accelerate the CPU's screen output to connect the card’s VGA or DVI output to a monitor or TV. This had no impact on the CPU, so no speed-ups were expected.

Now look at the GPU (top right). It has an embedded video processor, a RAMDAC, and its own video memory. This is a ‘full’ graphics card, but it’s not a modern GPU. In fact, it’s not even a GPU in the sense of a ‘GPU chip’ (see below), which can offload processing from the CPU.

A GPU is a ‘processing unit’, not a ‘display unit’.

It is a parallel processor, able to do many operations at once. This makes it very useful for certain types of computations, like image processing and machine learning, but not so well suited for sequential tasks like word processing.

A GPU’s strength lies in its ability to process large amounts of data in parallel. This makes it well-suited for tasks that can be broken down into many smaller, independent operations.

A GPU’s weakness is that it is not well-suited for tasks that require complex, sequential logic. This is because the GPU is designed to do many things at once, not one thing at a time.

A GPU’s other weakness is that it is not as good at controlling the flow of data as a CPU is. This is because the GPU is designed to process large amounts of data in parallel, not to control the flow of data.

In the end, a GPU is a great tool for certain types of computations, but not so well suited for others. It is up to the programmer to decide which tool to use for which task.

### MESA TODAY

Supported by the kernel, Mesa GL library is a 3D API wrapper for software drivers or for those that can be accelerated in hardware. It is now used by many operating systems (OS) to provide GPU acceleration.

In 1999, the initial version was open source by the SGI OpenVR group, with later development led by the Mesa 3D Graphics Library project. The library’s development is coordinated by the Mesa 3D Graphics Library project.

OpenGL is a C language API that lets you create an OpenGL context in a C program. It is used by many game engines and other 3D applications.

The API is available on many platforms, including Linux, Windows, and macOS. It is also available on many mobile devices.

The API is supported by many graphics cards, including those from NVIDIA, AMD, and Intel.

The API is used by many 3D applications, including games, CAD software, and scientific visualization tools.

The API is a powerful tool for creating 3D graphics and animations. It is a great choice for anyone who wants to create 3D content.

In a sense, Mesa is the same as OpenGL, but it is a C library rather than a C API. It is used to create OpenGL contexts in C programs. It is a powerful tool for creating 3D graphics and animations. It is a great choice for anyone who wants to create 3D content.

Mesa is a powerful tool for creating 3D graphics and animations. It is a great choice for anyone who wants to create 3D content. It is a powerful tool for creating 3D graphics and animations. It is a great choice for anyone who wants to create 3D content.

![](img/f20a68d91e56325c44e9a1405ca1923f_33_1.png)

An NVidia A100 GPU at Supercomputing. Photo: Dave Taht/CC-BY-SA.

We throw a Linux video card into two dimensions. But it’s a good trick if they can’t be caught by 3D. It also gives us an introduction to hardware and DirectX.

# X marks the spot

Most PC users know the X Window system of Unix (1996, a story that we look at next). Starting in the 1980s, X serves computers. X was designed for workstation display. It is designed to work in any environment — whether local hardware or remote servers. X’s development went hand-in-hand with many of the early Unix windowing environments. X has had a very long history with Unix, and as such its window manager has always been part of the OS. For a long time, there was no X server for the Microsoft Operating System (3.01, an early release of DOS), as the X project was a part of Unix development.

As the X server gained more support, the X development team looked at making an X server for the PC. This was a daunting task. It was eventually XFree86 that made X available to the PC platform in 1996. XFree86 was a fork of X11, which was the latest X release in 1994. The fork was done in 1995, and XFree86 was released in 1996. It was a huge amount of work to make X available on the PC platform. The first version of XFree86 only supported SVGA displays. SVGA was a standard for high resolution displays that was created by several manufacturers. SVGA displays could be connected to the PC using a VGA cable. SVGA displays were expensive, but they offered high resolution displays.

As the XFree86 project matured, support for more displays was added. SVGA was the first display standard supported by XFree86. VGA was the next display standard supported. VGA displays are much lower resolution than SVGA displays. As XFree86 matured, it also supported Xv and Xv-GLX. These were extensions to the X server that allowed for hardware accelerated 2D and 3D graphics.

![](img/f20a68d91e56325c44e9a1405ca1923f_34_0.png)

# Querying your 3D stack

Intel's numbering systems make no sense, but whatever your card there's plenty of demos to play with...

![](img/f20a68d91e56325c44e9a1405ca1923f_35_0.png)

As a long-time 3D enthusiast and developer, I remember from back when we were using the nVidia GeForce MX/Mon series. The cards were a range of graphics cards that had been specifically designed for gamers. From 2003 to 2005 the MX and MX2 series were some of the best graphics cards available. They were the fastest cards on the market and were supported by a number of the latest 3D applications such as Doom 3 and Call of Duty 2. But in 2005 the GeForce card series were replaced by the more powerful GeForce card series. The new cards were faster, more powerful, and had a range of new features that made them even more attractive to gamers.

- **Mesa Open Graphics**: This is a free, open-source implementation of the OpenGL API. It is developed by the Mesa project.
- **NVIDIA Optimus**: This is a technology that allows NVIDIA graphics cards to switch between the integrated and discrete GPU for improved performance and battery life.
- **AMD CrossFireX**: This is a multi-GPU technology that allows two or more AMD graphics cards to work together to improve performance.
- **Intel HD Graphics**: This is the integrated graphics that is built into Intel processors.

# AN ACCUMULATION OF ACRONYMS

Modern graphics cards are mini-clocks with thousands of transistors, working in parallel, and enabling them to do complex computing tasks far beyond the original intent of the card, which is to drive a monitor display. The more transistors on a card, the more complex the tasks it can perform, and the more complex the tasks it can perform, the more it will need to use the CPU to offload. CPU time is expensive, so the card will need to be very efficient in its use of the CPU. This is why a single card can have multiple cores, and why a single core can have multiple threads. The more threads a card can use, the more tasks it can perform in parallel. This is why a single card can have multiple cores, and why a single core can have multiple threads. The more threads a card can use, the more tasks it can perform in parallel.

- **Direct3D 12 (D3D12)**: This is a low-level API that provides direct access to the hardware. It is used in Windows 10 and later.
- **Vulkan**: This is a cross-platform API that provides direct access to the hardware. It is used in Windows, Linux, macOS, and Android.
- **OpenGL**: This is a cross-platform API that provides indirect access to the hardware. It is used in Windows, Linux, macOS, and Android.
- **OpenCL**: This is a cross-platform API that provides access to the hardware for general-purpose computing. It is used in Windows, Linux, macOS, and Android.
- **CUDA**: This is a proprietary API that provides access to the hardware for general-purpose computing. It is used in Windows and Linux.

In the end, it doesn't really matter which API you use, as long as you use it correctly. The most important thing is to understand the basics of how the hardware works, and to use the API in a way that makes the most sense for your application. This will ensure that you get the best possible performance from your hardware.
