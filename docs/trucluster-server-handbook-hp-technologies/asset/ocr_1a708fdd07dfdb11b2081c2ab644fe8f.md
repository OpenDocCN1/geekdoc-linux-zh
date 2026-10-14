# NOTE:

If you are using the csh shell, you will need to escape the "!" character like "\!". This is necessary to be able to print the "!" character. Omitting the "\" will result in an "": Event not found." error. Note further that the "Event" in the error message does not refer to an EVM event but is the C shell's way of saying that the command you were trying to recall was not found. The "!" is how you recall a command from your history list.

# 8.7.8 How Can I Send an Event from a Script?

You can post an event from a script by using the evmpost command from within your script. There is also a small excerpt of a script in the evmpost(1) reference page.

# 8.7.9 How Can I Format the Event Information I Receive?

Formatting event information can be done using the "-t" switch to the evmwatch, evmget, or evmshow commands. The "-t" enables you to create a "show-template" for the command. The format can use any valid EVM data item as defined in the EvmEvent(5) reference page. When using a data item in the "show-template", prefix it with "@". The data items are listed in uppercase in the EvmEvent(5) reference page, but you can use lowercase. Note that the "@a" is the actual event text with any variable values, referred to in the text, substituted in place of their references.

```
# evmget -A -t "@pid [@priority] @name: @a" -f "[prio > 600]"
- [700] sys.unix.binlog.hw.correctable_rpt_switch: Correctable error reporting state changed
- [700] sys.unix.binlog.hw.correctable_rpt_switch: Correctable error reporting state changed
302 [700] sys.unix.hw.net.niff.down: NIFF: node sheridan detected a failed network connection on network 192.168.0.69 via interface tu0
```

If you find that you are constantly using the same format, you may wish to define the format in the EVM_SHOW_TEMPLATE environment variable.

```
# export EVM_SHOW_TEMPLATE="@pid [@priority] @name: @a"
# evmget -A -f "[name *.hw]"
21667 [300] sys.unix.hw.dev_base_name_changed.tape__hwid.123: Device base name changed from unknown to tape0 (HWID=123)
21667 [300] sys.unix.hw.dev_base_name_changed.tape__hwid.124: Device base name changed from unknown to tape1 (HWID=124)
```