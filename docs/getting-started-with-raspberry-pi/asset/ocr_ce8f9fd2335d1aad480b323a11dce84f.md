Another way to use the RTC from user space is via the character device, `/dev/rtc`. Only one process is allowed to access this device at a time.

We discuss more about RTC drivers in Chapter 5 and Chapter 8. In Chapter 19, we develop an example user application that uses `/dev/rtc` to perform periodic work with microsecond precision.