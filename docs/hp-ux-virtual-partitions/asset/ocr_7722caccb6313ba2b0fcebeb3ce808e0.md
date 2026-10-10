Minimum: " 1"  
Maximum: "32767"  
Default: "2048"

Specify integer value.

# Description

"`msgseg`", multiplied by "`msgsz`", defines the total amount of shared-memory message space that can exist for all message queues, system-wide (not including message header space).

The related parameter, "`msgssz`" (message segment size in bytes), defines the number of bytes that are reserved for each message segment in any queue. When a message is placed in the queue, the length of the message determines how many "`msgssz`" segments are used for that message. Space consumed by each message in the queue is always an integer multiple of "`msgssz`".

"`msgseg`" (message segments) defines the number of these units that are available for all queues, system-wide.

"`msgssz`"

Specify message segment size to be used when allocating message space in message queues.

Acceptable Values:

Minimum: "1"  
Maximum: Memory limited  
Default: "8 bytes"

Specify integer value.

# Description

"`msgssz`", multiplied by "`msgseg`", defines the total amount of shared-memory message space that can exist for all message queues, system-wide (not including message header space).

"`msgssz`" specifies the size, in bytes, of the segments of memory space to be allocated for storing IPC messages. Space for new messages is created by allocating one or more message segments containing "`msgssz`" bytes each as required to hold the entire message.