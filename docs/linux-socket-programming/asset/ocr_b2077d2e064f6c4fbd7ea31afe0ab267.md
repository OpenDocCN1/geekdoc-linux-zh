# ## Data Flow Glitches

Communication between peers is not always clear. Each may assume that the other is supposed to talk first (network deadlock). Another problem is like being placed on hold forever: You are never sure that the person hasn't put you on hold and taken a coffee break for the rest of the day.

Starvation occurs when a requestor waits indefinitely for a response. The cause may include a bad network, slow peer, rebooted peer, and so on. In most cases, you can solve a starved receiver by programming a tickler, which is simply a message to remind the sender that your receiver program is still waiting.

The tickler should wait a period of time before getting impatient. You could include the last sequence ID sent and even a time stamp in the message. After hearing nothing from the sender, the receiver may reset the connection. This process does require the sender to understand the tickler and connection reset messages.

A network deadlock can happen when one of the messages is lost during a packet interchange. The sender waits for the reply, while the receiver still waits for the lost message. Your tickler could help break the deadlock as well. For example, in the packet interchange example, the receiver tickles your sender with the last sequence ID it got. Your program, in turn, retransmits the lost message.

# ## Juggling Tasks: A Multitasking Introduction

Going back to the sender and receiver programs, why use two programs? Why not use just one? Using one program is possible, but when you want to send and receive at the same time, you essentially need two programs.

Suppose that you had a distributed program (a program that uses the network as a multiprocessor) that processes image data very quickly. Your network uses several stages to process the image: image capturer, deflecker, smoother, quantizer, and serializer. Each of these is on a different computer, and the information flows from one stage to the next. The smoother receives data from the deflecker, processes the information, and passes it on to the quantizer. Each middle stage must receive and send nearly at the same time, like a bucket with a hole in the bottom.

In this example, you cannot easily combine two stages. Each stage has to be separate, so that the information going in does not get muddied with the results going out. Of course you could toss in the issue of image error: How do you get an error message *up* the cascade?

Dividing the task into well-defined responsibilities is part of the concept of *multitasking*. You can run several programs at the same time in their own contexts to ensure that the inputs and outputs never mingle. This avoids corrupted results. The examples you see in this chapter use a form of multitasking because they run as separate programs.

The programs are actually similar enough that you could merge them into one so that they talk to themselves. In that case and to simplify the interactions, you must create a separately running task for each, indicating which one sends the first message.

Multitasking is integrally embedded in network programming. [Chapter 8, "Choosing when to Wait for I/O."](Chapter 8, "Choosing when to Wait for I/O.") discusses multitasking in greater detail.