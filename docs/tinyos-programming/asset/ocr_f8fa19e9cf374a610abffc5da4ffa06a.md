```
command storage_len_t getSize();
}
```

Listing 6.40 The LogRead interface

The log implementations guarantee that the data written by a single LogWrite.append operation will be either fully present, or fully absent, so we know that the log will not contain any partial summaries. So we could for instance read the log from the beginning, in 512-byte chunks (the size of one summary) and know that we have read a valid summary sample.

Log storage also provides limited seek support. The LogRead and LogWrite interfaces contain the following command

```
command storage_cookie_t currentOffset();
```

which returns a cookie that represents the position at which the next read or append will start. These cookies are not offsets in the log volume; they just contain enough information to allow the log storage implementation to find that position in the log. LogRead’s split-phase seek command can seek to such cookies.

This would allow, e.g. the FlashSampler application, to report the position of the samples to a PC, and then reread specific samples on demand.

# 6.6 Exercises

+   1. Port the anti-theft application to a different platform than the micaz, by writing new theft detection code tailored to the particular sensors you have available.
+   2. Extend the anti-theft application so that motes notice the theft reports sent by neighboring motes and report them locally by blinking LED 1.
+   3. Extend the anti-theft application so that the user can select between the light-level (DarkC) and acceleration (MovingC) theft detection methods, and switch the LED 0 blinking on or off.
+   4. Add code to FlashSampler to transfer samples and sample summaries to the PC over the serial port. Allow the user to (re)request specific sample summaries or erase all the summaries.