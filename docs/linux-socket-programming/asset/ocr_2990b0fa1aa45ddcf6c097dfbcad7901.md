Chapter 5. Understanding the Network Layering 72

Model

Solving the Network Challenge 73

Open Systems Interconnection (OSI) Network Model .... 77

Internet Protocol Suite 81

Fundamental Differences Between OSI and IP 84

What Services What? 85

Summary: From Theory to Application 85

Part II: The Server Perspective and Load Control 86

Chapter 6. A Server Primer 86

Mapping the Socket: The Server's General Program 86

Flow 86

A Simple Echo Server 88

General Rules About Defining Protocols 94

An Extended Example: An HTTP Directory Server 96

Summary: The Server's Basic Elements 98

Chapter 7. Dividing the Load: Multitasking 99

Defining Multitasking: Processes Versus Threads 100

Beating the Clock: Race Conditions and Mutexs 121

Controlling Children and Killing Zombies 124

Extending Current Clients and Servers 127

Calling External Programs with the 127

Server 127

Summary: Distributing the Process Load 130

Chapter 8. Choosing when to Wait for I/O 130

I/O Blocking: Why? 131

When Do I Block? 132

Alternatives to I/O Blocking 132

Comparing the Different I/O Programming 133

Interactions 133

Polling I/O 134

Asynchronous I/O 138

Solving Unwanted I/O Blocking with 143

and 143

Implementing Timeouts 145

Summary: Choosing the I/O Techniques 146

Chapter 9. Breaking Performance Barriers 147

Creating the Servlets Before the Client Arrives 147

Extending Control with a Smart Select 153