# Device Example: Real Time Clock

Let's now take the example of an RTC chip connected to an embedded controller over the I²C bus. The connection diagram is shown in Figure 8.3.

![](bbox=[0.25, 0.19, 0.75, 0.22])

![](bbox=[0.15, 0.22, 0.85, 0.48])

Assume that the I²C slave address of the RTC is 0x60 and that its register space is organized as shown in Table 8.2.

| **Register Name** | **Description** | **Offset** |
|---|---|---|
| RTC_HOUR_REG | Hour counter | 0x0 |
| RTC_MINUTE_REG | Minute counter | 0x1 |
| RTC_SECOND_REG | Second counter | 0x2 |
| RTC_STATUS_REG | Flags and interrupt status | 0x3 |
| RTC_CONTROL_REG | Enable/disable RTC | 0x4 |

Let's base our driver for this chip on the EEPROM driver discussed previously. We will take the I²C client driver architecture, slave registration, and I²C core functions for granted and implement only the code that communicates with the RTC.

When the I²C core detects a device having the RTC's slave address (0x60) on the I²C bus, it invokes myrtc_attach(). The invocation train is similar to that for eep_attach() in Listing 8.5. Assume that you have to perform the following chip initializations in myrtc_attach():

+   1. Clear the RTC status register (RTC_STATUS_REG).