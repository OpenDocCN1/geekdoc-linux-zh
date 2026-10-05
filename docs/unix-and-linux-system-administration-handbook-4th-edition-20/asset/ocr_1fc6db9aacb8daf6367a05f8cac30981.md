# 20.12 SENDMAIL PERFORMANCE

sendmail has several configuration options that improve performance. Although we have scattered them throughout the chapter, we expand on the most important ones in this section. These are options and features you should consider if you run a high-volume mail system (in either direction). Actually, if you really need to send 1,000,000 mail messages an hour and you aren't a spammer, your best bet might be to use the commercial side of sendmail, Sendmail, Inc.

# Delivery modes

sendmail has four basic delivery modes: background, interactive, queue, and defer. Each represents a tradeoff between latency and throughput. Background mode delivers the mail immediately but requires sendmail to fork a new process to do it. Interactive mode also delivers immediately, but delivery is by the same process and makes the remote side wait for the results. Queue mode incoming mail for delivery by a queue runner at some later time. Defer mode is similar to queue mode, but it also defers all map, DNS, aliases, and forwarding-ups. Interactive mode is rarely used. Background mode favors lower latency, and defer or queuing favor higher throughput. The delivery mode is set with the option confDELIVERY_MODE and defaults to background.

# Queue groups and envelope splitting

Queue groups let you create multiple queues for outgoing mail and control the attributes of each queue group individually. Queue groups are used with an envelope-splitting feature that distributes an envelope with many recipients (such as a message sent to a mailing list) across multiple queue groups. Several configuration-pr are used with queue groups. See the O'Reilly sendmail book or the cf/README file for examples and details.

# Queue runners

sendmail forks copies of itself to perform the actual transport of mail. You can control how many copies are running at any time and how many copies are attached to each queue group. By using this feature, you can balance the activities of sendmail and the operating system on your busy mail hubboxes.

Three sendmail options control the number of queue runner daemons processing each queue:

+   * MAX_DAEMON_CHILDREN option sets the total number of copies of the sendmail daemon that are allowed to run at any one time, including those running queues and those accepting incoming mail.
* MAX_QUEUE_CHILDREN option sets the maximum number of queue runners allowed at one time.