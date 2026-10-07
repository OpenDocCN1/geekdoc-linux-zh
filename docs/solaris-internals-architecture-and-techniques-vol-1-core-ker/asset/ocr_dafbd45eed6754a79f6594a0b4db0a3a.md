handle the setup and checking required for syncing dirty pages with their backing store. The functions, described in Table 13-3, set up pages so that they can be passed to device driver block I/O handlers.

# Table 13-3 Solaris 7 vnode Paging Functions from vm/pvn.h

| Function | Description |
|---|---|n| pvn_getdirty() | Queries whether a page is dirty. Returns 1 if the page should be written back (the iolock is held in this case), or 0 if the page has been dealt with or has unlocked. |
| pvn_plist_init() | Releases the iolock on each page and the page lock to shared after new pages have been created or read. |
| pvn_read_done() | Unlocks the page after read is complete. The function is normally called automatically by pageio_done() but may need to be called if an error was encountered during a read. |
| pvn_read_kluster() | Finds the range of contiguous pages within the supplied address / length that fit within the provided vnode offset / length that do not already exist. Returns a list of newly created, locked pages ready for I/O. Checks that clustering is enabled by calling the segop_kluster() method for the given segment |
| pvn_write_done() | Unlocks the page after write is complete. For asynchronous writes, the function is normally called automatically by pageio_done() when an asynchronous write completes. For synchronous writes, pvn_write_done() is called after pageio_done to unlock written pages. It may also need to be called if an error was encountered during a write.