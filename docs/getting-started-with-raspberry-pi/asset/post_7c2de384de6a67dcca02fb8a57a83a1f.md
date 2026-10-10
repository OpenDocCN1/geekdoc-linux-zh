
## USB and Bluetooth Keyboards

The USB specifications related to *human interface devices* (HID) stipulate the protocol that USB keyboards, mice, keypads, and other input peripherals use for communication. On Linux, this is implemented via the *usbhid* USB client driver, which is responsible for the USB HID class (\(0x03\)). usbhid registers itself as an input device driver. It conforms to the input API and reports input events appropriate to the connected HID.

To understand the code path for a USB keyboard, revert to Figure 7.3 and modify the hardware-specific left half. Replace the keyboard controller in the Input Hardware box with a USB controller, serio with the USB core layer, and the Input Device Driver box with the usbhid driver.

For a Bluetooth keyboard, replace the keyboard controller in **Figure 7.3** with a Bluetooth chipset, serio with the Bluetooth core layer, and the Input Device Driver box with the Bluetooth hidp driver.

USB and Bluetooth are discussed in detail in Chapter 11, "Universal Serial Bus," and Chapter 16, "Linux Without Wires," respectively.

## Mice

Mice, like keyboards, come with different capabilities and have different interfacing options. Let's look at the common ones.

### PS/2 Mice

Mice generate relative movements in the X and Y axes. They also possess one or more buttons. Some have scroll wheels, too. The input device driver for PS/2-compatible legacy mice relies on the serio layer to talk to the underlying controller. The input event driver for mice, called *mousedev*, reports mouse events to user applications via */dev/input/mice*.

#### Device Example: Roller Mouse

To get a feel of a real-world mouse device driver, let's convert the roller wheel discussed in Chapter 4, "Laying the Groundwork," into a variation of the generic PS/2 mouse. The "roller mouse" generates one-dimensional movement in the Y-axis. Clockwise and anticlockwise turns of the wheel produce positive and negative relative Y coordinates respectively (like the scroll wheel in mice), while pressing the roller wheel results in a left button mouse event. The roller mouse is thus ideal for navigating menus in devices such as smart phones, handhelds, and music players.

The roller mouse device driver implemented in **Listing 7.3** works with windowing systems such as X Windows. Look at `roller_mouse_init()` to see how the driver declares its mouse-like capabilities. Unlike the roller wheel driver in **Listing 4.1** of Chapter 4, the roller mouse driver needs no `read()` or `poll()` methods because events are reported using input APIs. The roller interrupt handler `roller_isr()` also changes accordingly. Gone are the housekeepings done in the interrupt handler using a wait queue, a spinlock, and the `store_movement()` routine to support `read()` and `poll()`.

In Listing 7.3, the leading + and – denote the differences from the roller wheel driver implemented in Listing 4.1 of Chapter 4.

**Listing 7.3. The Roller Mouse Driver**

```c
#include <linux/input.h>
#include <linux/interrupt.h>

/* Device structure */
struct {
    /*...*/
    struct input_dev dev;
} roller_mouse;

static int __init
roller_mouse_init(void)
{
    /* Allocate input device structure */
    roller_mouse->dev = input_allocate_device();

    /* Can generate a click and a relative movement  */
    roller_mouse->dev->evbit[0] = BIT(EV_KEY) | BIT(EV_REL);

    /* Can move only in the Y-axis  */
    roller_mouse->dev->relbit[0] = BIT(REL_Y);

    /* My click should be construed as the left button
       press of a mouse  */
    roller_mouse->dev->keybit[LONG(BTN_MOUSE)] = BIT(BTN_LEFT);

    roller_mouse->dev->name = "roll";

    /* For entries in /sys/class/input/inputX/id/ */
    roller_mouse->dev->id.bustype = ROLLER_BUS;
    roller_mouse->dev->id.vendor = ROLLER_VENDOR;
    roller_mouse->dev->id.product = ROLLER_PROD;
    roller_mouse->dev->id.version = ROLLER_VER;

    /* Register with the input subsystem */
    input_register_device(roller_mouse->dev);
}

/* Global variables  */
/* -spinlock_t roller_lock = SPIN_LOCK_UNLOCKED; */
/* -static DECLARE_WAIT_QUEUE_HEAD(roller_poll); */

/* The Roller Interrupt Handler  */
static irqreturn_t
roller_interrupit(int irq, void *dev_id)
{
    int i, PA_t, PA_delta_t, movement = 0;

    /* Get the waveforms from bits 0, 1 and 2
       of Port D as shown in Figure 7.1 */
    PA_t = PORTD & 0x07;

    /* Wait until the state of the pins change.
       (Add some timeout to the loop)  */
    for (i=0; (PA_t==PA_delta_t); i++){
        PA_delta_t = PORTD & 0x07;
    }

    movement = determine_movement (PA_t, PA_delta_t);

    /* -spin_lock(&roller_lock); */
    /* -/* Store the wheel movement in a buffer for */ */
    /* -   later access by the read()/poll() entry points  *-/ */
    /* -store_movements(movement); */
    /* -spin_unlock(&roller_lock); */
    /* -/* Wake up the poll entry point that might have */ */
    /* -   gone to sleep, waiting for a wheel movement  *-/ */
    /* -wake_up_interruptible(&roller_poll); */

    if (movement == CLOCKWISE) {
        input_report_rel(roller_mouse->dev, REL_Y, 1);
    } else if (movement == ANTICLOCKWISE) {
        input_report_rel(roller_mouse->dev, REL_Y, -1);
    } else if (movement == KEYRESSED) {
        input_report_key(roller_mouse->dev, BTN_LEFT, 1);
    }
    input_sync(roller_mouse->dev);

    return IRQ_HANDLED;
}
```

### Trackpoints

A trackpoint is a pointing device that comes integrated with the PS/2-type keyboard on several laptops. This device includes a joystick located among the keys and mouse buttons positioned under the spacebar. A trackpoint essentially functions as a mouse, so you can operate it using the PS/2 mouse driver.

Unlike a regular mouse, a trackpoint offers more movement control. You can command the trackpoint controller to change properties such as sensitivity and inertia. The kernel has a special driver, drivers/input/mouse/trackpoint.c, to create and manage associated sysfs nodes. For the full set of track point configuration options, look under /sys/devices/platform/1042/serioX/serioY/.

### Touchpads

A touchpad is a mouse-like pointing device commonly found on laptops. Unlike conventional mice, a touchpad does not have moving parts. It can generate mouse-compatible relative coordinates but is usually used by operating systems in a more powerful mode that produces absolute coordinates. The communication protocol used in absolute mode is similar to the PS/2 mouse protocol, but not compatible with it.

The basic PS/2 mouse driver is capable of supporting devices that conform to different variations of the bare PS/2 mouse protocol. You may add support for a new mouse protocol to the base driver by supplying a protocol driver via the psmouse structure. If your laptop uses the Synaptics touchpad in absolute mode, for example, the base PS/2 mouse driver uses the services of a Synaptics protocol driver to interpret the streaming data. For an end-to-end understanding of how the Synaptics protocol works in tandem with the base PS/2 driver, look at the following four code regions collected in Listing 7.4:

- The PS/2 mouse driver, drivers/input/mouse/psmouse-base.c, instantiates a psmouse_protocol structure with information regarding supported mouse protocols (including the Synaptics touchpad protocol).
- The psmouse structure, defined in drivers/input/mouse/psmouse.h, ties various PS/2 protocols together.
- synaptics_init() populates the psmouse structure with the address of associated protocol functions.
- The protocol handler function synaptics_process_byte(), populated in synaptics_init(), gets called from interrupt context when serio senses mouse movement. If you unfold synaptics_process_byte(), you will see touchpad movements being reported to user applications via mousedev.

**Listing 7.4. PS/2 Mouse Protocol Driver for the Synaptics Touchpad**

```c
/*drivers/input/mouse/psmouse-base.c*/
/* List of supported PS/2 mouse protocols */
static struct psmouse_protocol psmouse_protocols[] = {
{
    .type    = PSMOUSE_PS2,   /* The bare PS/2 handler */
    .name    = "PS/2",
    .alias   = "bare",
    .maxproto = 1,
    .detect  = ps2bare_detect,
},
/* ... */
{
    .type    = PSMOUSE_SYNAPTICS,  /* Synaptics TouchPad Protocol */
    .name    = "SynPS/2",
    .alias   = "synaptics",
    .detect  = synaptics_detect,   /* Is the protocol detected? */
    .init    = synaptics_init,     /* Initialize Protocol Handler */
},
/* ... */
};

/*drivers/input/mouse/psmouse.h*/
/* The structure that ties various mouse protocols together */
struct psmouse {
    struct input_dev *dev;  /* The input device */
    /* ... */
    /* Protocol Methods */
    psmouse_ret_t (*protocol_handler)
                (struct psmouse *psmouse, struct pt_regs *regs);
    void (*set_rate)(struct psmouse *psmouse, unsigned int rate);
    void (*set_resolution)
                (struct psmouse *psmouse, unsigned int resolution);
    int (*reconnect)(struct psmouse *psmouse);
    void (*disconnect)(struct psmouse *psmouse);
    /* ... */
};

/*drivers/input/mouse/synaptics.c*/
/* init() method of the Synaptics protocol */
int synaptics_init(struct psmouse *psmouse)
{
    struct synaptics_data *priv;
    psmouse->private = priv = kmalloc(sizeof(struct synaptics_data),
            GFP_KERNEL);
    /* ... */
    /* This is called in interrupt context when mouse */
    /* movement is sensed */
    psmouse->protocol_handler = synaptics_process_byte;
    /* More protocol methods */
    psmouse->set_rate = synaptics_set_rate;
    psmouse->disconnect = synaptics_disconnect;
    psmouse->reconnect = synaptics_reconnect;
    /* ... */
}
```
