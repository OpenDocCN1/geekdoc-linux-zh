
## PART III Looking at Sockets Objectively

### 11 Saving Time with Objects
- The Software Engineering Evolution
- Step-by-Step Functional Programming
- Hiding Implementation with Modular Programming
- Not Needing the Details: Abstract Programming
- Getting Close to Nature Through Object Programming
- Reaching Programming Nirvana
- Reusing Your Work
- Strengthening Reuse with Pluggability
- Laying the Object Foundation
- Implementation Encapsulation
- Behavior Inheritance
- Data Abstraction
- Method Polymorphism
- Object Features
- The Class or Object
- Attributes
- Properties
- Methods
- Access Rights
- Relationships
- Extending Objects
- Templates
- Persistence
- Streaming
- Overloading
- Interfaces
- Events and Exceptions
- Special Forms
- Record/Structure
- Function Bag
- Language Support
- Supporting Versus Enabled Versus Oriented
- How to Map Objects to Non-Object Languages
- Summary: Object-Oriented Thinking

### 12 Using Java's Networking API
- Exploring Different Java Sockets
- Programming Clients and Servers
- Implementing Messengers
- Sending to Multiple Destinations
- Connecting Through I/O
- Classifying the I/O Classes
- Converting Between I/O Classes
- Configuring the Java Socket
- Shared Java-Socket Configurations
- Java Multicast-Specific Configurations
- Multitasking the Programs
- Threading a Class
- Adding Threads to a Class
- Synchronizing Methods
- Implementation Limitations
- Summary: Java-Style Network Programming

### 13 Designing and Using a C++ Socket Framework
- Why Use C++ for Sockets Programming?
- Simplifying Sockets Interfacing
- Hiding Implementation Details
- Deploying Reusable Components with Easy to Use Interfaces
- Demonstrating the Framework Design Processes
- Laying Out the Framework
- Defining the General Features
- Grouping into Major Components
- Creating the Framework Hierarchy
- Defining Each Class’s Capabilities
- Testing the Socket Framework
- The Echo Client/Server
- Multitasking Peer-to-Peer
- Implementation Limitations
- Sending Unknown/Undefined Messages
- Adding Multitasking
- Summary: A C++ Socket Framework Simplifies Programming

### 14 Limits to Objects
- Mind Over Objects
- Beginning on the Right Foot
- A Blender Is Not an Object
- Separating Analysis from Design
- The Right Level of Detail
- The Inheritance Explosion
- Reuse-Misuse
- Using C++’s friend Correctly
- The Overloaded Operator
- Objects Don’t Solve Everything.
- Fads Come and Evolve
- Inheritance Infection
- Unreachable Code
- Complexity Give and Take
- Simplifying Programs with Established Interfaces
- Multiple Inheritance Conundrum
- Code Bloat
- Project Management Dilemma
- Getting the Right People at the Right Time
- WISCY (“Whiskey”) Phenomenon
- Testing (Dis-)Integration
- Summary: Walk Carefully on Shale

## Part IV Advanced Sockets—Adding Value

### 15 Network Encapsulation with Remote Procedure Calls (RPCs)
- Revisiting the OSI Model
- Comparing Network and Procedural Programming
- Language Limits
- Holding Connected Sessions
- Supplying Middleware Methods
- Stubbing Network Calls
- Adding the Service Call Implementation
- Implementing the Presentation Layer
- Creating RPCs with rpcgen
- rpcgen’s Interface Language
- Creating Non-Stateless Calls with Open Connections
- Diagnosing the State Problem
- Remembering Where You Are
- Following a Specific Route
- Recovering from a State Failure
- Summary: Creating an RPC Toolkit

### 16 Adding Security to Network Programs and SSL
- Giving Permission to Work
- Levels of Identification
- Forms of Interchange
- The Problem with the Internet
- Everything Is Visible
- Forms of Intrusion/Attack
- TCP/IP Crackability
- Securing a Network Node
- Restricting Access
- Firewalls
- Demilitarized Zones (DMZs)
- Securing the Channel
- Encrypting the Messages
- What Are the Available Encryption Types?
- Published Encryption Algorithms
- Problems with Encryption
- Secure Sockets Layer (SSL)
- Using OpenSSL
- Creating an SSL Client
- Creating an SSL Server
- Summary: The Secure Server

### 17 Sharing Messages with Multicast, Broadcast, and MBone
- Broadcasting Messages to a Domain
- Revisiting IP Structure
- Programming to Enable Broadcasting
- Broadcasting Limitations
- Multicasting Messages to a Group
- Joining Multicast Groups
- Sending a Multicast Message
- How the Network Provides Multicasting
- Getting Out the Multicast Message
- Multicasting Limitations
- Summary: Efficient Message Sharing

### 18 The Power of Raw Sockets
- When Would You Use Raw Sockets?
- Exposing the ICMP
- Controlling the IP Header
- Speeding Through the Physical Network
- What Are the Limitations?
- Putting Raw Sockets to Work
- Selecting the Right Protocol
- Creating an ICMP Packet
- Calculating a Checksum
- Controlling the IP Header
- Third-Party Traffic
- How Does Ping Work?
- The MyPing Receiver
- The MyPing Sender
