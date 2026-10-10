# VMS VERSION

The VMS version does not set the file ti.

VMS C Standard I/O and RMS may interact to modify file contents unexpectedly.

The VMS version does not support invocation as **rzCOMMAND**. The current VMS version does not support XMODEM, XMODEM-1k, or YMODEM.

According to the VMS documentation, the buffered input routine used on the VMS version of *rz* introduces a delay of up to one second for each protocol transaction. This delay may be significant for very short files. Removing the “#define BUFREAD” line from *rz.c* will eliminate this delay at the expense of increased CPU utilization.

The VMS version causes DCL to generate a random off the wall error sssage under so error conditions; this is a result of the incompatibility of the VMS “exit” function with the Unix/MSDOS standard.