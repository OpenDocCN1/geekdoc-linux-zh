+   - InnoDB_buffer_pool_read_ahead_rnd
+     The number of random read-aheads initiated by InnoDB. These occur when InnoDB must read a large part of a table in non-sequential order.
+   - InnoDB_buffer_pool_read_ahead_seq
+     The number of sequential read-aheads initiated by InnoDB. These occur when InnoDB performs sequential full-table scans.
+   - InnoDB_buffer_pool_read_requests
+     The number of logical read requests issued by InnoDB.
+   - InnoDB_buffer_pool_reads
+     The number of single-page reads done due to not being able to perform a logical read from the InnoDB buffer pool.
+   - InnoDB_buffer_pool_wait_free
+     The number of times InnoDB had to wait for writes to the buffer pool to be flushed. Writes usually are done in the background, but InnoDB must perform a wait if no pages are available when it needs to read a page or create a new one.
+   - InnoDB_buffer_pool_write_requests
+     The number writes to the InnoDB buffer pool.
+   - InnoDB_data_fsyncs
+     The number of sync-to-disk operations performed by InnoDB.
+   - InnoDB_data_pending_fsyncs
+     The number of pending InnoDB data sync-to-disk operations.
+   - InnoDB_data_pending_reads
+     The number of pending InnoDB data-read operations.
+   - InnoDB_data_pending_writes
+     The number of pending InnoDB data-write operations.
+   - InnoDB_data_read
+     The number of bytes read by InnoDB.
+   - InnoDB_data_reads
+     The number of InnoDB data-read operations.
+   - InnoDB_data_writes
+     The number of InnoDB data-write operations.
+   - InnoDB_data_written
+     The number of bytes written by InnoDB.
+   - InnoDB_dblwr_pages_written
+     The number of pages written to the InnoDB doublewrite buffer.