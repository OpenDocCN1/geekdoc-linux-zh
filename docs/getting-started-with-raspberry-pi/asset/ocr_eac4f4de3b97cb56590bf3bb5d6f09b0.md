+   2. A bottom thread springing from the interrupt service routine that collects data from the device

Figure 6.7 shows these threads associated with the read data flow. The interrupt handler queues the *receive_buf() method (n_touch_receive_buf() in our example) as a task. You can override this behavior by setting the tty->low_latency flag.

# Figure 6.7. Line discipline read path.

![](bbox=[0.15, 0.25, 0.85, 0.6])

The touch controller and the processor communicate using a specific protocol described in the controller's data sheet. The driver implements this communication protocol using an FSM as indicated earlier. Listing 6.4 encodes this FSM as part of the *receive_buf()* entry point, n_touch_receive_buf().

# Listing 6.4. The n_touch_receive_buf() Method