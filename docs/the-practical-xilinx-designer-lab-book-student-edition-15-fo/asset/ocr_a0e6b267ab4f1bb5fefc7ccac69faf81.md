(h) Another read operation was performed. The value of 71 that was loaded in step (c) was finally read and the rdptr was incremented. The FIFO is no longer completely full, so the full flag is reset to zero.

From the example, you can see that the reader of the FIFO gets the data in the same order as it was entered by the writer. The advantage of using the FIFO is that it decouples the reader and writer so they do not have to do their operations in lock-step. For instance, a sensor might provide four bytes of data at 1 µs intervals, but each burst occurs only once a second. Without a FIFO, each data byte would have to be transmitted as soon as it arrived at a rate of 8 bits/byte × 1 byte/µs = 8 bits/µs = 8,000,000 bits/sec. Instead, a FIFO could be used to accept the high-speed sensor bursts and then dole them out slowly to a transmitter that operates at a rate of 8 bits/byte × 4 bytes/s = 32 bits/s. The decoupling of the sensor and the transmitter by the FIFO allows you to build a transmitter based on the average data rate from the sensor rather than the peak rate. And the equipment needed to transmit at 32 bits/s is much cheaper than what is needed to do 8 megabytes/s.

Now that you know how a FIFO operates and the advantages it provides, you have to return to the question, "How do I build one?" First, you should define the interface as shown in Figure 8.14. There are two ports:

Write port: The write port consists of an 8-bit in bus for entering the data bytes. A low pulse on the wr control line writes the data into the FIFO. The full status output informs the data supplier if the FIFO is full and cannot accept any more data.

Read port: The read port has an 8-bit out bus for sending out the data bytes. A low level on the rd line places the next byte of data from the FIFO onto the out bus. The empty status output informs the data consumer if the FIFO is empty and no data is available.

The final signal in the interface is the reset, which has the obvious function of initializing the FIFO to the empty state.

From the interface description, you can work inward to create a simple block diagram like the one in Figure 8.15. The components you will need are as follows:

RAM: Obviously, you need static RAM to store the data.

rdptr: The read pointer is a counter that increments in the wrap-around sequence 0, 1, ..., N−1, 0, 1 so that all N memory locations can be addressed. A read operation must cause the pointer to be incremented, but not if the FIFO is empty. If that happened, then the write pointer would be one behind the read pointer and the FIFO would interpret this to mean the FIFO had N−1 data bytes in it. Then these N−1 bytes of old data would be erroneously read out as if they were new.