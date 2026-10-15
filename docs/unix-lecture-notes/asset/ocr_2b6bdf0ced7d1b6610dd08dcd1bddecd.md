outside of the computer are things like traffic lights, hand gestures that mean "please stop, taxi driver" or "give me the check", alarm clock rings, or warning lights like "you're about to run out of gas". They do not have contents. It is enough that they have identity, so a particular signal type has well-defined meaning. When a combatant raises a white flag, the enemy knows that this signal means "I give up." In UNIX, a signal is simply an integer with a mnemonic name. For example, SIGINT is the interrupt signal.

# 5.3.1 Typing Ctrl-C at a Terminal

When you type a Ctrl-C, the effect is to terminate the currently running process. Why? When you type the Ctrl-C, the character code for it is sent by hardware and then, within the kernel, to the terminal's device driver. The device driver checks the character code and sees that it matches the INTR code[3]. Since it knows this is a control character that is supposed to cause delivery of an interrupt signal, it checks whether the isig attribute is set for the terminal. If isig is set, then the corresponding signal must be delivered, which is SIGINT, so it calls the signal subsystem of the kernel to notify it to send the SIGINT signal to all processes whose control terminal[4] is the one that received the Ctrl-C. If any of these processes has not explicitly notified the kernel of how it wants to handle this signal, it will terminate upon receipt of the signal, because by default, processes are killed if they do not catch SIGINT. Soon we shall see that a process can declare what the disposition of a delivered signal should be while it is running.

# 5.3.2 Sources of Signals

All signals are sent by the kernel to processes. There is no other way for a process to receive a signal; the kernel is like the central signal processing station inside the machine. The kernel will send a signal to one or more processes if it receives a request to do so. Requests can come from a few different types of sources.

The terminal A user can type a key combination that causes the terminal driver to ask the kernel to send a signal. This is an asynchronous signal, since it can arrive at a process at any time, independent of what the process might be doing. Examples include Ctrl-C, Ctrl-Z, Ctrl-S.

Hardware Hardware exceptions can generate signals. The kernel detects when the exception occurs and sends a signal to the offending process. These may be synchronous or asynchronous. Synchronous events are things such as floating-point exceptions, illegal instructions, addressing exceptions (such as attempts to access addresses outside of the process's address space), and other events generally caused by the process itself. They are synchronous because if the process is run again, they will occur again at the same point in the process's execution. Asynchronous events are things like power loss and terminal hang-ups.

Software Software conditions can generate signals when something noteworthy happens. This can happen when out-of-band data arrives over a network connection, or when a process writes to a pipe after the reader of the pipe has terminated, or when an alarm clock set by the process expires.

3In SunOS it is INTR. On other systems, it might be VINTR.

4The operating system keeps track of which processes are attached to which terminals.