# Checking Logs

All logging information for Exim is written to three log files that can be found in /var/log/exim4/mainlog, rejectlog, and paniclog. The first of these, mainlog, contains entries for all events, including normal events such as message delivery. The second, rejectlog, contains entries for rejected messages. The third contains about configuration or other errors, and is usually empty unless a serious problem has occurred. Every entry in these files generally starts with a timestamp.

Entries in the mainlog will often include a string of 15 characters, such as 1E9PTU-0003JN-OY. This is the message identifier for the log entry is related to. Immediately after the message identifier there will be a two-character string. Table 25-1 details what those strings mean.

# Table 25-1
Exim Log File Messages

| Symbol | Description | Explanation |
| :--- | :--- | :--- |
| <= | Message arrival | These entries show messages coming into Exim, generally through SMTP or local IPC. |
| => | Message delivery | These entries show deliveries, whether they are to a local mailbox or to a remote host using SMTP or other transport. |
| -> | Additional addresses in message delivery | These entries show delivery to additional addresses for messages that have already been delivered to another recipient (logged with an => entry). |
| ** | Delivery failure | These entries show permanent delivery errors. Errors such as indicate that the message has been removed from the message queue and in most cases a DSN (Delivery Status Notification) has been generated and sent to the original message sender. |
| == | Delivery deferral | These entries show temporary delivery errors. The system will continue to retry sending until delivery succeeds, or a permanent failure occurs as a result of a retry timeout. |