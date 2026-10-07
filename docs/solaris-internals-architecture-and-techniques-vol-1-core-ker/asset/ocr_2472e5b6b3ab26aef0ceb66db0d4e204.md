# Sessions and Process Groups

+   - A link to a PID structure

The session ID is derived in the same way as the PGID for a process. That is, the session structure will link to the PID structure of the process that is attached to the control terminal, the login shell in most cases. Note that daemon processes, which do not have a control terminal, will have a NULL vnode pointer in the session structure. All processes will thus link to a session structure, but processes without control terminals will not have the vnode link; that is, they have no connection to a control device driver.

Figure 8.25 provides the big picture, illustrating a login session with a process group and showing the links to the related data structures.

![](bbox=[0.135, 0.345, 0.885, 0.605])

Figure 8.25 Process and Session Structure Links