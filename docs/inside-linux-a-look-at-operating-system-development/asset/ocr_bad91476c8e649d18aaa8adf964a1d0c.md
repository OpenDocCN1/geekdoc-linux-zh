In addition, one should realize that security is most importantly a mind-set, not a set of programs and procedures. Security can be lost through willful or uncaring acts by users and system administrators.

That being said, we can now discuss what basic mechanisms are available to protect a system. Most basically, they control what can be done by whom.

# 4.5.1 Authorization

Conceptually, authorization can be described in terms of a three dimensional matrix shown in Figure 4.22. The three indices are agent, object and action. Each element has the value “permitted” or “denied” (or perhaps “produces exception signal”).

![](bbox=[0.14, 0.42, 0.89, 0.73])

Figure 4.22: Access matrix

In one case, the agents are processes, the objects are files and directories and the actions are system calls such as *open, read, write,* and *create.*

In another case the agents are processes, the objects are process *states* and the actions are *signal, wait* and *kill.*

This matrix is very sparse—in part because the actions aren’t appropriate to the object and in part because not all agents have equal