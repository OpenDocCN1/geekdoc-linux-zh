# 174 CHAPTER 9 Ftrace

in the block layer the entry represents. These values translate a trace action, blktr_act as defined in the $|LINUX_SRC|include/uapi/linux/blktr_api.h header as an ASCII character. Table 9.1 lists the values and their meanings. In the case this field contains an additional value, not listed in Table 9.1, follow the citations, which point to the source code and define and explain possible value.

Whereas the sixth column describes the action performed at the block layer, the seventh column describes the actual I/O operation. These values are much straight forward, with “W” standing for a write, with “R” standing for a read, with “S” standing for a sync, and so on. Finally, the eighth column provides the details of the operation, which depends on the action being

# Table 9.1 Encodings of blk Trace Entry Actions (Howells, 2012; Rosted et al., 2009, b)

| Encoding | Action | Meaning |
| --- | --- | --- |
| Q | __BLK_TA_QUEUE | I/O request added to queue |
| M | __BLK_TA_BACKMERGE | I/O request merged into an existing operation (at the end) |
| F | __BLK_TA_FRONTMERGE | I/O request merged into an existing operation (at the front) |
| G | __BLK_TA_GETRQ | Allocate a request in the queue |
| S | __BLK_TA_SLEEPQ | Process blocked awaiting request allocation |
| R | __BLK_TA_REQUEUE | Request was not completed and is placed back onto the queue |
| D | __BLK_TA_ISSUE | Request entry issued to device driver |
| C | __BLK_TA_COMPLETE | I/O request complete |
| P | __BLK_TA_PLUG | Request entry in key awaiting more requests to improve throughput of block device |
| U | __BLK_TA_UNPLUG_IO | Plugged request has been released to be issued to device driver |
| I | __BLK_TA_INSERT | Request inserted into run queue |
| X | __BLK_TA_SPLIT | Request needed to be split into two separate requests due to a hardware limitation |
| B | __BLK_TA_BOUNCE | A hardware limitation prevented data from being transferred from the block device to memory, a bounce buffer was used (which requires extra data copying) |
| A | __BLK_TA_REMAP | Request mapped to the raw block device |