![](bbox=[0.05, 0.09, 0.85, 0.28])

Figure 5.9: Normal interrupt service

interrupts enabled, it can be quite extensive. Because of this, bottom half code can be thought of as a limited capability process.

The mouse driver offers one example of normal interrupt service. This is still a very simple device because the device and the user process are somewhat isolated from one another. The interrupt service routine accesses several device registers and updates a structure containing the current mouse position. Reading the mouse simply returns the contents of this structure, there is no need to co-ordinate with the interrupt service routine. Because the interrupt service routine takes a bit longer to execute. it uses the normal type of interrupt service.

The serial driver shows another aspect of the normal interrupt service, the “bottom half” code. Like the mouse driver, the serial driver takes an interrupt whenever new data are received. It places incoming characters in a dynamic buffer area called the “flip queue” and signals that other code should continue the processing. Signalling is done through the `queue_task` and `queue_task_irq_off` kernel subroutines. (The term “bottom half” comes from the idea that it is at the bottom half of the device driver.)

The utility of this scheme is that *any* kernel subroutine can be established as bottom half code. As drivers are initialized then can establish work queues and they can create entries which can be placed on the queue. In the case of the serial driver, the code which runs as the bottom half is common to a large number of serial hardware device drivers. This higher level driver takes care of all terminal I/O processes the data which was put in the flip queue. That code will eventually call `wake_up`