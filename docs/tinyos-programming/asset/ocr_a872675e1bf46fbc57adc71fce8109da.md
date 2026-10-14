For test_serial_msg_t, the basic constructor and methods of the mig-generated TestSerialMsg class are:

+   - TestSerialMsg(): create a new (fields initialised to zero) test_serial_msg_t value.
+   - static int offset_counter(): Return the offset (in bytes) of the counter field in a test_serial_msg_t structure.
+   - get_counter(): Return the value of the counter field.
+   - set_counter(int value): Modify the value of the counter field.

# 7.2.1 Sending and receiving mig-generated packets

The net.tinyos.message package provides a class MoteIF (for "mote interface") that makes it simple to transmit and receive messages specified by a mig-generated class.

Before using MoteIF, you need to open a connection to your base station mote. This is done by calling the net.tinyos.packet.BuildSource.makePhoenix method, which takes as argument a packet source name. This packet source name specifies how you reach the base station mote (e.g. through a serial port) and all the relevant parameters (e.g. device name, baud rate, etc). In the rest of this section, we will use "serial@COM1;telosb" as our packet source, which denotes serial communication over serial port COM1 at the normal Telos mote baud rate (115 200 baud). Most Java programs that use MoteIF take a command-line argument that specifies the actual packet source. Section 7.4 discusses packet sources, and their motivation, in more detail.

Using MoteIF and mig, the code to transmit test_serial_msg_t messages is quite simple, as this simplified excerpt from the TestSerial.java file shows. Transmission of consecutive packets is performed using MoteIF's send method, which takes an object of a mig-generated class as argument:

```
public class TestSerial ... {
    private MoteIF moteIF;
    ...
    public void sendPackets() {
        int counter = 0;
        // Create uninitialized TestSerialMsg
        TestSerialMsg payload = new TestSerialMsg();
        try {
            while (true) {
                System.out.println("Sending packet," + counter);
                payload.setCounter(counter);
                moteIF.send(0, payload); // send payload to mote
                counter++;
                try {Thread.sleep(1000);}
                catch (InterruptedException exception) ()
            }
        }
```

> See the mig documentation for a complete description of the generated constructors and methods.