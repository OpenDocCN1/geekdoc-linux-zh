This feature provides support for the UNIX 98 pseudoterminal numbering convention, which is superior to the traditional Linux pseudoterminal number convention. You should keep the default.

If you keep the default, you are asked the following question, to set the maximum number of UNIX 98 PTYs that can be in use by the system:

# Maximum number of Unix98 PTYs in use (0-2048) (CONFIG_UNIX98_PTY_COUNT) [256]

For most cases, the default value should be sufficient.

# Mouse Support (not serial mice) (CONFIG_MOUSE) [Y/n/?]

This feature allows you to use a mouse with terminals capable of using such a device. The default is recommended.

# QIC-02 tape support (CONFIG_QIC02_TAPE) [N/y/m/?]

If you have QIC-02 tape, you can choose to add support for it here.

# Watchdog Timer Support (CONFIG_WATCHDOG) [N/y/?]

If you want to create a watchdog timer such that it can reboot the system in case of a failure, answer y here. If you do enable this feature, you have to create a special device called /dev/watchdog (major,minor=130,0) by using the mknod program. Then, you can use a watchdog daemon program that will write to this special device every minute. If the kernel detects that the device has not been written to by the daemon for one minute, it will reboot the system.

# /dev/nvram support (CONFIG_NVRAM) [N/y/m/?]

This feature allows you to create a special device /dev/nvram, which gives you read/write access to nonvolatile memory in the real time clock. Unless you know what you are doing, keep the default.

# Enhanced Real Time Clock Support (CONFIG_RTC) [N/y/?]

This feature allows you to create a special device, /dev/rtc, which can be used to access the real-time clock in your system. Unless you know what you are doing, keep the default.