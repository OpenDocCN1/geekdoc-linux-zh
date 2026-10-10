+   2. Start the RTC (if it is not already running) by turning on appropriate bits in the RTC control register (RTC_CONTROL_REG).

To do this, let's build an `i2c_msg` and generate I2C transactions on the bus using `i2c_transfer()`. This transfer mechanism is exclusive to I2C and is not SMBus-compatible. To write to the two RTC registers referred to previously, you have to build two `i2c_msg` messages. The first message sets the register offset. In our case, it's 3, the offset of RTC_STATUS_REG. The second message carries the desired number of bytes to the specified offset. In this context, it ferries 2 bytes, one each to RTC_STATUS_REG and RTC_CONTROL_REG.

Code View:

```
```c
#include <linux/i2c.h> /* For struct i2c_msg */
int myrtc_attach(struct i2c_adapter *adapter, int addr, int kind)
{
    u8 buf[2];
    int offset = RTC_STATUS_REG;  /* Status register lives here */
    struct i2c_msg rtc_msg[2];

    /* Write 1 byte of offset information to the RTC */
    rtc_msg[0].addr = addr;      /* Slave address. In our case,
                                     this is 0x60 */
    rtc_msg[0].flags = I2C_M_WR; /* Write Command */
    rtc_msg[0].buf = &offset;    /* Register offset for the
                                     next transaction */
    rtc_msg[0].len = 1;          /* Offset is 1 byte long */

    /* Write 2 bytes of data (the contents of the status and
       control registers) at the offset programmed by the previous
       i2c_msg */
    rtc_msg[1].addr = addr;      /* Slave address */
    rtc_msg[1].flags = I2C_M_WR; /* Write command */
    rtc_msg[1].buf = &buf[0];    /* Data to be written to control
                                     and status registers */
    rtc_msg[1].len = 2;          /* Two register values */
    buf[0] = 0;                  /* Zero out the status register */
    buf[1] |= ENABLE_RTC;        /* Turn on control register bits
                                     that start the RTC */

    /* Generate bus transactions corresponding to the two messages */
    i2c_transfer(adapter, rtc_msg, 2);

    /* ... */
    printk("My RTC Initialized\n");
}
```
```

Now that the RTC is initialized and ticking, you can glean the current time by reading the contents of RTC_HOUR_REG, RTC_MINUTE_REG, and RTC_SECOND_REG. This is done as follows:

Code View:

```
```c
#include <linux/rtc.h> /* For struct rtc_time */
int
```
```