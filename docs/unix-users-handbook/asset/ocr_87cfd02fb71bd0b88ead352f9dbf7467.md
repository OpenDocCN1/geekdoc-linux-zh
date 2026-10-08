# NET PRINT

**NET PRINT** - This command lists print jobs and shared queues.

The following is a command summary of the **NET PRINT** com-mand.

```
C:\ NET PRINT /?

NET PRINT \\\computename\sharename
[\\\[computename\] job# [/HOLD | /RELEASE | /DELETE]
```

Some commonly used options follow:

+   - **\\computename**
The *computename* sharing the print queues.

+   - **sharename**
The print queue *sharename*.

+   - **job#**
The unique number assigned to a print job.

+   - **/HOLD**
The job is assigned a status of *HOLD*, which means that it will not be printed until it is released or deleted.

+   - **/RELEASE**
Releases a print job so that it can be printed.

+   - **/DELETE**
Deletes a print job from the print queue.