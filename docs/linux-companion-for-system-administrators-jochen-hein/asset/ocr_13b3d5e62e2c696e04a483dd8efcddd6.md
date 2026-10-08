# 52 SYSTEM START-UP

If, in addition, timeout is not set, the computer halts at this point and waits for input.

restricted
Cancelar some of the restrictions set by password. Any configuration can be booted, but no input of parameters is allowed. You can use this option, for example, to prevent activation of the single-user mode.

serial=parameter_string
Allows system control via a serial connection, that is, LILO accepts input both from the keyboard and from the connected terminal. Sending a Break via the connection corresponds to pressing the Shift key at the console and causes the boot: prompt to be displayed on the screen.

When access via a serial connection is activated, all configurations should be protected by means of password if access via the serial is less secure than access to the console itself; for example, when a modem is connected to the serial interface. The format of the parameter_string has the following syntax: port,bpsparitybits The last three specifications can be omitted; if one of these specifications is not made, the subsequent ones must be omitted. If only the port is specified, the comma must be omitted too. On my system, I use serial=1,9600n8 for a 9600-baud terminal on /dev/ttyS1.

When serial=0n8 is set, the value for delay is automatically set to two. With the setting serial=0,2400n8, the first serial interface is initialized with the default values. Together with some kernel modifications and adaptations of the init program, it is thus possible to use a simple terminal as console.

timeout=tsecs
Determines the time LILO waits for keyboard input. If no key is pressed within the specified time, the default image is loaded; if no specification has been created for default=, this is the first image listed. Correspondingly, the password check is also aborted if during this time no input was made. The default value for timeout= is infinite.

verbose=level
This is used to activate error and diagnostic messages. The higher this value, the more messages are output.