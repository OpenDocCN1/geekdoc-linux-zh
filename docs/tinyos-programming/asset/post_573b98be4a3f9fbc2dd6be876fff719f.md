
for the small, low-power microcontrollers motes have. Furthermore, TinyOS has very aggressive systems and mechanisms for saving power.

TinyOS makes building sensor network applications easier. It provides a set of important services and abstractions, such as sensing, communication, storage, and timers. It defines a concurrent execution model, so developers can build applications out of reusable services and components without having to worry about unforeseen interactions. TinyOS runs on over a dozen generic platforms, most of which easily support adding new sensors. Furthermore, TinyOS’s structure makes it reasonably easy to port to new platforms.

TinyOS applications and systems, as well as the OS itself, are written in the nesC language. nesC is a C dialect with features to reduce RAM and code size, enable significant optimizations, and help prevent low-level bugs like race conditions. Chapter 2 goes into the details on how nesC differs significantly from other C-like languages, and most of this book is about how to best use those features to write robust, efficient code.

### 1.2.1 What TinyOS provides

At a high level, TinyOS provides three things to make writing systems and applications easier:

- a component model, which defines how you write small, reusable pieces of code and compose them into larger abstractions;
- a concurrent execution model, which defines how components interleave their computations as well as how interrupt and non-interrupt code interact;
- application programming interfaces (APIs), services, component libraries and an overall component structure that simplify writing new applications and services.

The component model is grounded in nesC. It allows you to write pieces of reusable code which explicitly declare their dependencies. For example, a generic user button component that tells you when a button is pressed sits on top of an interrupt handler. The component model allows the button implementation to be independent of which interrupt that is – e.g. so it can be used on many different hardware platforms – without requiring complex callbacks or magic function naming conventions. Chapter 2 and Chapter 3 describe the basic component model.

chapter, Chapter 11) can have race conditions, of course: nesC detects possible data races at compile-time and warns you.

Finally, TinyOS itself has a set of APIs for common functionality, such as sending packets, reading sensors, and responding to events. Uses of these are sprinkled throughout the entire book, and presented in more detail in Chapter 6 and Appendix 1. In addition to programming interfaces, TinyOS also provides a component structure and component libraries. For example, Chapter 12 describes TinyOS’s Hardware Abstraction Architecture (HAA), which defines how to build up from low-level hardware (e.g. a radio chip) to a hardware-independent abstraction (e.g. sending packets). Part of this component structure includes resource locks, covered in Chapter 11, which enable automatic low-power operation, as well as the component libraries that simplify writing such locks.

TinyOS itself is continually evolving. Within the TinyOS community, “Working Groups” form to tackle engineering and design issues within the OS, improving existing services and adding new ones. This book is therefore really a snapshot of the OS in time. As Chapter 12 discusses and Appendix 1 presents, TinyOS has a set of standard, stable APIs for core abstractions, but this set is always expanding as new hardware and applications emerge. The best way to stay up to date with TinyOS is to check its web page www.tinyos.net and participate in its mailing lists. The website also covers advanced TinyOS and nesC features which are well beyond the scope of this book, including binary components, over-the-air reprogramming services, debugging tools, and a nesC reference manual.

### 1.3 Example application

To better understand the unique challenges faced by sensor networks, we walk through a basic data-collection application. Nodes running this application periodically wake up, sample some sensors, and send the data through an ad hoc collection tree to a data sink (as in Figure 1.1). As the network must last for a year, nodes spend 99% of their time in a deep sleep state.

In terms of energy, the radio is by far the most expensive part of the node. Lasting a year requires telling the radio to be in a low power state. Low power radio implementation techniques are beyond the scope of this book, but the practical upshot is that packet transmissions have higher latency. [23]

Figure 1.3 shows the four TinyOS APIs the application uses: low power settings for the radio, a timer, sensors, and a data collection routing layer. When TinyOS tells the application that the node has booted, the application code configures the power settings on the radio and starts a periodic timer. Every few minutes, this timer fires and the application code samples its sensors. It puts these sensor values into a packet and calls the routing layer to send the packet to a data sink. In practice, applications tend to be more complex than this simple example. For example, they include additional services such as a management layer which allows an administrator to reconfigure parameters and inspect the state of the network, as well as over-the-air programming so the network
