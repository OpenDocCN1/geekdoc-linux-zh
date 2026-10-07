
# Chapter 19 Test Using Linux USB ................................................................................................ 275

- Linux USB Unit Test Driver .................................................................................................................... 276
Linux USB Functional Test ...................................................................................................................... 279
Storage USB Gadget ................................................................................................................................ 279
Serial USB Gadget ..................................................................................................................................... 281
USB Network Gadget ................................................................................................................................ 283
HID (Human Interface Devices) USB Gadget ................................................................................ 284
Summary ................................................................................................................................................... 285
More Reading ....................................................................................................................................................... 285

# Appendix USB Regression Tool ................................................................................................ 287

- Overview of USB Regression Tool .................................................................................................... 288
Script Definitions ...................................................................................................................................... 289
Generic USB Functions ................................................................................................................................................ 289
Utility Functions ..................................................................................................................................... 291
Summary ................................................................................................................................................... 292

# Index .......................................................................................................................................................... 293

# INTRODUCTION

Before starting a new task, you generally do research so you can avoid mistakes. In the computer realm, bootstrap sessions provide a head start and help you minimize mistakes and surprises. As an example, to design a protocol stack, build a bootstrap session so you can understand the protocol specification and the system on which it is to be developed.

This book discusses how the Linux host and device stacks are designed and how different Linux USB modules export interfaces to pass on information. Understanding the pains of test development, this book provides comprehensive coverage of the necessary frameworks available on Linux for USB systems to effectively debug, test, and interface with USB devices.

# WHAT YOU'LL FIND IN THIS BOOK

This book discusses the internal interface application programming interfaces (APIs) and data structures of the USB stack and offers practical examples of how Linux USB modules interface within the Linux system.

- Linux is becoming the de facto standard for Linux to train and explore. This book is a practical guide book to exploring Linux USB.
- This book explains a platform developer’s perspective of Linux USB drivers: the gadget driver for a USB device and the host controller driver development for a host.

# Introduction

- You will find topics that enhance your understanding of user mode programming of the Linux USB framework and easy methods to use it with USB devices.

- This book also explores methods to test and debug USB devices using USB. The CD accompanying the book contains an exclusive tool for USB testing.

# Who This Book Is For

This book is for students interested in exploring the emerging embedded Linux market and Linux internals. The book teaches them Linux USB internals and enables them to complete a project based on the Linux USB subsystem. The book also further their understanding of software stack design by exposing the blocks, interfaces, and data structures of the Linux USB system.

This book is also for engineers who take up Linux-USB development. In the industry, the trend while assigning jobs is creating module and module experts. It is common to move them to different modules.

Finally, this book is for managers of the Linux platform who want to know the features or analyze the complexity of the Linux USB. This book’s visual representations act as a definite bootstrap session.

# How This Book Is Organized

The book is organized into four major parts: USB Host, USB Device, USB OTG, and Miscellaneous Linux USB Subsystems. Before getting into parts, the initial three chapters provide a quick overview of USB in general and how to manage the Linux USB framework. Part I explores the Linux USB host framework that implements USB requirements. The USB device implementation referred to as gadget is explored in Part II. Dual role On-the-Go (OTG) devices are covered in Part III. Part IV covers various frameworks available on Linux that you can effectively use for USB development. The book narrates the Linux USB system using the Linux 2.6.34 kernel.

Following is a more detailed breakdown of the content in each chapter.

Chapter 1, “USB and Linux: Introduction,” introduces the history and path of USB and Linux and how both technologies are placed in the embedded space.

Chapter 2, “USB: An Overview,” is a snapshot of the USB specification, covering only parts that are essential from a software perspective.

Chapter 3, “Overview of the Linux USB Subsystem,” explores the various configuration options available in the Linux USB subsystem so that you can configure features you’re interested in.

Chapter 4, “Linux USB Host Driver,” provides an overview of the various blocks of the Linux USB host subsystem and sets the tone for the subsequent chapters that explore the Linux USB host framework.

Chapter 5, “USB Device Notification,” discusses how the device connection and disconnection information is passed on to other modules and within the Linux USB framework and how to use it.

Chapter 6, “Device File System,” explores the essential framework required to create Virtual File System (VFS) files along the Linux USB host framework that creates them. The Linux driver model represents devices as VFS files, and the Linux USB subsystem creates VFS files for the devices connected to it.

Chapter 7, “Power Management,” looks at the power management framework of the Linux USB subsystem. Power management is an essential framework for embedded systems running on battery. The Linux kernel has implemented different power management techniques as part of it.

Chapter 8, “Hub,” discusses the Linux USB hub design requirement and offers a practical example. A hub between a USB device and a host providing electrical, connection/disconnection, and transaction translation.

Chapter 9, “Generic Driver,” explains the core data structures and interfaces of the Linux USB host framework.

Chapter 10, “Host Driver for Embedded Controller,” explores the USB host controller driver requirements and the design requirements to implement them. The USB specification, such as the Enhanced Host Controller Interface (EHCI), the Universal Host Controller Interface (UHCI), or the Open Host Controller Interface (OHCI), defines the host controller requirements.

Chapter 11, “Linux USB Gadget Driver,” provides an overview of the Linux USB gadget design and the generic USB stack design and sets the tone for the subsequent chapters of the gadget driver.

Chapter 12, “Peripheral Device Controller Driver,” delves into the peripheral device controller design requirements and demonstrates a sample device controller implementation.
