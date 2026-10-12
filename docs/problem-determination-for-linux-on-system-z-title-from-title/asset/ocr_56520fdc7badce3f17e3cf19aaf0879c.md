> **Note:** var/log/messages on Linux does not have the messages that are shown during Linux hang, down, or reboot.

# 8.3.2 Investigating hardware-related messages

Hardware error messages in z/VM basically have an error code and its meaning. Check the messages and code manual of each component for your version of z/VM.

We have no manual about hardware messages in Linux. Searching the meaning of messages from past cases is a good approach of investigation. You can search in the z/VM Technical Q&A library and Bugzilla. Linux source code would have its meaning.

Here we provide some sample hardware error messages.

# Example of hardware error messages for DASD

Sense data is an error returned from a SCSI device. Sense data is available in the sense buffer. For more information about sense data, see: 

http://www.linux.org/docs/1dphowto/archived/SCSI-Programming-HOWTO/SCSI-Programming-HOWTO-10.html

The sense data description is displayed directly in the message. Example 8-6 shows a sample of this sense data.

![](bbox=[0.14, 0.58, 0.85, 0.78])