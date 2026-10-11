The process of moving the control file between queues is a simple matter of changing its filename extension to reflect the current queue number.

The following table outlines the message-processing functions associated with each queue.

# **Table 8-4**

| Filename | Function |
| :--- | :--- |
| xxxxxxx:000 | Queue 0 is the prep queue. NMAP makes sure the control file meets all processing requirements and the AntiVirus Agent scans the data file. |
| xxxxxxx:001 | Message is processed by the AntiSpam Agent and/or the List Agent. |
| xxxxxxx:002 | Message is processed by the Alias Agent and/or the AutoReply Agent. |
| xxxxxxx:003 | Message is processed by the Rule Agent. |
| xxxxxxx:004 | Not currently used by a NetMail agent; might be used by a third-party or custom agent. |
| xxxxxxx:005 | Message is processed by the Calendar Agent. |
| xxxxxxx:006 | Messages to recipients within the messaging system are delivered by the NMAP Agent. |