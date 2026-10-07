# File System I/O

Table 13-10 describes the segmap statistics.

# Table 13-10 Statistics from the seg_map Segment Paged Driver

| Field Name | Description |
| --- | --- |
| fault | The number of times segmap_fault was called, usually as a result of a read or write system call. |
| faulta | The number of times the segmap_faulta function was called. It is called to initiate asynchronous I/O on a file. |
| getmap | The number of times the segmap_getmap function was called. It is called by the read and write system calls each time a read or write call is started. It sets up a slot in the seg_map segment for the requested range on the file. |
| get_use | The number of times getmap found an empty slot in the segment and used it. |
| get_re | The number of times getmap found a valid mapping for the file and offset already in the seg_map segment. |
| get_reuse | The number of times getmap deleted the mapping in a nonempty slot and created a new mapping for the file and offset requested. |
| get_unused get_nofree | Not used—always. The number of times a request for a slot was made and none available on the internal free list of slots. This number is usually zero because each slot is put on the free list when release is called at the end of each I/O. Hence, free slots are usually available. |
| rel_async | The slot was released with a delayed I/O on it. |
| rel_write | The slot was released as a result of a write system call. |
| rel_free | The slot was released, and the VM system may be needed again but to free it and retain its file/offset information. These pages are placed on the cache tail so that they are not the first to be reused. |
| rel_abort | The slot was released and asked to be removed from the seg_map segment as a result of a failed aborted write. |
| rel_dontneed | The slot was released, and the VM system told the page because it won't be needed again. These pages are placed on the cache list head so they will be reused. |
| released | The slot was released and the release was not affected by rel_abort, rel_async, or rel_write. |
| pagecreate | Pages created in the segmap_pagecreate function. |