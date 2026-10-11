# **FIGURE 7.1** Conceptual Redo Log Buffer mechanism

![](bbox=[0.28, 0.15, 0.85, 0.58])

# ## Tuning the Redo Log Buffer

U nlike the Shared Pool and Database Buffer Cache, the Redo Log Buffer is not managed by an LRU mechanism. Instead of the conveyor belt concept of the LRU List, the Redo Log Buffer's management mechanism can be thought of as funnel, where transaction redo information enters at the top of the funnel and is then occasionally emptied out the bottom of the funnel by the LGWR background process. To keep up with the volume of incoming Redo Log Buffer entries, LGWR is prompted to write the contents of the Redo Log Buffer to disk whenever any of the following events occur:

+   - Whenever an application user issues a **COMMIT** command
+   - Every three seconds