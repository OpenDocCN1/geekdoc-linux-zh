Table A.1   Perl Functions (continued)

| **Function** | **Description** |
|---|---|
| msgctl | *msgctl*(KEY, FLAGS)<br> Calls msgget system call. Returns the message queue ID number or, if undefined, an error.<br> See System V IPC.<br> See also msgget(2). |
| msgrcv | *msgrcv*(MSQID, VAR, MSG_SIZE, TYPE, FLAGS)<br> Calls the msgrcv system call. Receives a message from the message queue, stores the message in VAR. MSG_SIZE is the maximum message size, and TYPE is the message type.<br> See System V IPC.<br> See also msgrcv(2). |
| msgsnd | *msgsnd*(ID, MSG, FLAGS)<br> Calls the msgsnd system call. Sends the message MSG to the message queue. MSG must begin with the message type. The pack function is used to create the message.<br> See System V IPC.<br> See also msgsnd(2). |
| my | *my* TYPE EXPR : ATTRIBUTES<br> *my* EXPR : ATTRIBUTES<br> *my* TYPE EXPR<br> *my* EXPR<br> Variables declared with the my function are made private; i.e., they exist only within the innermost enclosing block, subroutine, eval, or file. Only simple scalars, complete arrays, and hashes can be declared with my. TYPE and ATTRIBUTES optional and experimental at this time. |
| new | *new* CLASSNAME LIST<br> *new* CLASSNAME<br> Not a built-in function but a constructor method defined by the CLASSNAME module for creating CLASSNAME-type objects. Convention taken from C++. |
| next | *next* LABEL<br> Starts the next iteration of the innermost or loop labeled with LABEL. Like the C continue function. |
| no | *no* MODULE LIST<br> If a pragma or module has been imported with use, the no function says you don't want to use it anymore. |
| not | *not* EXPR<br> Logically negates the truth value of EXPR. |